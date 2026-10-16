# Fog window study reference

Accepted source snapshot: October 10, 2026, commit `71a83b3` in the Natural Effects source project (`ambershen/dirty-window`). Entry: `?mode=steam` or `?mode=fog`. Inspect current files when adapting; older fog modules describe a different iteration.

## Source map and composition

- `src/fog.ts`: background, blurred veil, cached mist texture, clearing mask, stroke lifecycle, controls, and scene composition.
- `src/fog.css`: fullscreen scene and collapsible Temporary Canvas controls.
- `src/gestures/FogCamera.ts`: camera reflection, pinch writing, open-palm wiping, coordinate crop, and release callbacks.
- `src/gestures/FogBreath.ts`: experimental microphone adapter.
- `src/gestures/hand.ts`: hand features and openness classification.

The camera takes precedence over a selected image while available. Without either, a neutral linear gradient is used. The foreground is the veil with the clearing mask removed, composited over the clear scene. Dirty Level scales foreground opacity. The current clear-mask contribution is capped by a 0.95 compositing alpha, so clearing is not perfectly transparent through the veil.

## Accepted tuning

Dirty Level defaults to 100%, Temperature to 50%, and brush radius to seven CSS pixels. Hold and Fade controls were removed; internal recovery still holds for five seconds after release and fades over approximately thirty seconds with spatial variation and a smoothstep envelope. Do not claim recovery was removed.

The main canvas DPR is capped at 1.5. Clearing uses seventeen cached radial brush variants and segment stamps spaced no more than seven CSS pixels apart. The mask is rebuilt roughly every 50 ms; active marks do not age. Released marks are eventually pruned. Very long uninterrupted strokes still accumulate many marks; compact history if adapting this for installations.

Warmth reduces blur and veil opacity. There are no droplets, refractive beads, or gravity trails. Mist cloud alpha was reduced to approximately 0.035 for light clouds and 0.025 for dark clouds; grain alpha is below five out of 255. Baked radial background lights and circular recovery nuclei were removed after conspicuous light spots appeared at low density. These values belong to this study, not every fog material.

## Gesture and breath status

Pinch writes; releasing pauses; an open palm wipes broadly. Palm wiping uses the palm center and a size-dependent radius of 55–160 CSS pixels. See `FogCamera.ts` for the crop transform shared with the mirrored reflection.

Breath detection uses microphone RMS and a tonal-peak rejection heuristic, with a 1.2-second initial ambient calibration, input meter, device selector, and sensitivity control. It clears the center, not a detected mouth location. The user reported poor breath sensitivity; microphone selection and thresholds were revised, but reliable detection was not established. This is not a trained breath classifier.

The user requested a more natural wiping sound. This fog implementation has no restored wiping playback; do not present that request as completed or copy unrelated audio as an accepted solution.

## Regression scenarios

Test Dirty Level at 0%, 5%, and 100% with Temperature at 0%, 50%, and 100%. Near-zero density should not reveal synthetic spotlights, and maximum temperature must not introduce tiny droplets. Verify both camera and image backgrounds, full gesture recovery, and a change from pinch to palm to idle. Inspect source and target device rather than assuming browser permissions or microphone behavior transfer between devices.

## Source availability

The source map refers to [Natural Effects application](https://github.com/ambershen/dirty-window), a separate application. Its code and media are not bundled here. Snapshot commit identifiers document provenance and may not be publicly available. If the source is unavailable, use the behavioral guidance and tuning examples without assuming access to those files.
