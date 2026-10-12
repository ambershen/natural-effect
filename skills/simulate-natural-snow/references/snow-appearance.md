# Snow appearance recipe

## Accepted visual direction

The final user feedback was positive after the surface became whiter and denser. Earlier variants resembled ice: sparse prominent crystals, blue-gray outlines, procedural ridges, and visible glitter were the main failure modes. The following values are starting points from that study, not material constants.

Use an opaque near-white base around RGB (0.985, 0.989, 0.995), broad soft illumination, and low-contrast local shading. Example ambient shading was 0.86 + 0.20 * diffuse. Keep subtle long-scale terrain variation; remove repetitive ripples and high-frequency noise from the geometric normal.

Bake two seeded layers of randomly positioned and rotated six-arm crystals into a transparent texture:

- Dense underlayer: approximately one crystal per 14 CSS square pixels, radius 0.8–2.5 CSS pixels.
- Upper layer: approximately one per 68 CSS square pixels, radius 1.8–4.4 CSS pixels.
- Draw each arm with a pair of small diagonal branches. Use broad translucent white strokes over a very faint pale gray-blue edge, rather than a dark outline.
- Example upper edge RGBA (191,204,212,0.14), white core alpha 0.92; underlayer edge alpha 0.10 and white core alpha 0.82.
- Keep texture coordinates stationary in surface space. Clamp texture size (the study used a 2048-pixel longest edge and scale up to 1.5). Rebuild only on relevant size or material changes.

Composite the texture through the material shader so compression fades the distinct crystal structure. A useful intact fraction is `1 - smoothstep(0.02, 0.85, compaction)`, with texture strength interpolated between 0.18 for compressed and 0.65 for loose snow. Fresh coverage restores loose texture through the same compaction state. Avoid an independent opaque overlay that hides impression depth.

## Readable snowfall

The included `assets/snowflake-1.svg` through `snowflake-3.svg` are original six-arm crystals with slightly different branch positions. Load images once, then draw cached images with Canvas transforms or equivalent instancing. Wait for successful image decoding/loading before drawing.

The accepted browser setup used 90 flakes with nominal radius 7–13 CSS pixels, scaled by altitude from 0.65 to 1.4. This gives approximately 9–36 pixels of sprite diameter; the crystal itself has transparent margins. Tune density to viewport area for new implementations.

Use white branches with a restrained blue-gray edge for white-background legibility. Avoid a detached drop shadow. Vary position, angle, size, and rotation independently. Gentle flutter should not flatten the branches into narrow lines. Fade flakes in overhead and blend them into the surface at landing; do not simply replace a visible flake with another fully opaque sprite.

## Reference and provenance

The user suggested the [p5.js Snowflakes example](https://p5js.org/examples/Classes-And-Objects-Snowflakes/). It demonstrates particle-system snowfall, not a deformable powder surface. Its page identifies CC BY-NC-SA 4.0 licensing. This skill records general particle concepts and original implementation choices; it does not include that example's code. No p5.js dependency was added to the study.

Source map in the original application: `src/effects/GranularRenderer.ts` for surface shading and cached crystals, `public/textures/snowflake-*.svg` for airborne artwork, and `src/sand.ts` for snowfall. These paths are optional reference locations; the skill works without that application.
