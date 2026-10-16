---
name: simulate-natural-ice
description: Design or refine interactive thin ice over water, including faint friction writing, irregular pressure fractures, and restrained recording-based ice sounds. Use for touch, mouse, or gesture-driven ice experiences, including adaptations of the Natural Effects ice study.
---

# Simulate Natural Ice

Build thin ice over water that responds to touch with barely visible writing, irregular pressure fractures, and quiet natural recordings. Treat this as an artistic interaction model, not a physically validated simulation. The aesthetic choices of the original study are listed under [Study preset](#study-preset-natural-effects); adapt them when the user asks for a different material or look.

## Material and interaction

Separate three responses rather than making every movement break or erase the ice:

- **Glide:** immediate tracking, a soft damp contact patch and faint reflection. No bright white pen line or spray of particles from an ordinary fingertip.
- **Write/rub:** slow movement or repeated passes gradually thin the surface frost. Reveal a little muted underwater light through a feathered, uneven mask. Fast strokes are nearly invisible; repeated strokes accumulate but never become a clear hole or opaque ink. Let the marks slowly refrost. Make writing difficult through friction accumulation, not input lag.
- **Press:** near-stationary contact accumulates load; cracks extend progressively from the contact in several unequal directions. Nearby existing seams widen and irregular plates settle slightly. Slow writing should not accidentally count as stationary pressure.

For ordinary phone touch, use dwell as a pressure proxy and say so when relevant. Pen pressure may supplement it. Do not claim to measure hand force on hardware that does not provide it. A camera adaptation must explicitly map a tracked gesture to contact/load; do not assume the current touch implementation already supports it.

## Appearance and fracture geometry

Use cloudy depth, trapped bubbles, fine frost grain, and subtle plate-to-plate shading. References showed connected, irregular boundaries with changing widths, angular bends, branching, dark depth and whitish fracture lips.

Make neighboring plates share exactly the same rough boundary. A clipped Voronoi partition with shared perturbed edges is a useful starting point; avoid an obvious uniform grid. New contact fractures should grow along jagged paths over time, with unequal lengths and delayed side branches. Avoid one straight slash, symmetrical starbursts, or a regular polygon appearing as a detached sticker. Preserve damage on release and provide an explicit reset. Keep writing and crack state independent.

## Sound

Use real, appropriately licensed ice/frost recordings. Distinguish studio recordings of real material from outdoor recordings and synthetic audio; do not describe them interchangeably. Store local files and source/license credits. A recorded sound can still feel artificial when scheduled poorly.

- Sliding: one quiet continuous rubbing take with smoothly movement-controlled gain. Fade quickly when motion stops. Avoid frequent overlapping grains or a loud constant scraping loop.
- Fracture: discrete load/growth events, a small release followed optionally by a deeper break. Alternate real takes and preserve recorded tails. Avoid replaying the same “crunch” every few hundred milliseconds, artificial pitch sweeps, or sound continuing indefinitely on fully grown cracks.
- Do not consume a fracture sound event before its buffer is ready or playback is eligible; a retry should remain possible without advancing the audible damage stage.
- Leave silence and headroom. Keep spatial movement restrained. Softer filtering and lower gain are useful tuning controls, not substitutes for suitable source material.
- Unlock/resume audio synchronously within a real user gesture before fetch/decode awaits. Offer an icon mute/retry control. Stop voices on reset, loss of focus, or teardown; preserve valid multi-touch lifecycles. Test interruption/resume on the target phone.

## Verification

Read the current implementation before adjusting it. Verify fast versus slow writing, retracing, refrosting, stationary press, release, reset, mute, and multi-touch cleanup. Check that repeated rubs remain translucent and that a stationary hold does not produce endlessly repeating audio. Check a cold audio start as well as warmed playback. Keep cached textures and bounded history suitable for mobile rendering.

Use a browser preview for visible interaction checks and a build/type check appropriate to the changed code. Listening on the target phone is needed to judge sound quality: successful decoding and no console errors prove plumbing, not naturalness. Report what was actually tested.

## Study preset (Natural Effects)

These are the accepted choices of the original study, not general rules:

- Gray-white, subtly translucent ice. Blue was tried and rejected.
- A snowflake button resets the surface.
- Minimal, fullscreen presentation: explain gestures in chat rather than adding instructional text to the artwork.

## Related skills and references

When designing a camera or shared input adapter, `natural-motion-interaction` can help with coordinate alignment, contact identity, smoothing, and gesture transitions. It is optional; this ice skill remains self-contained. `simulate-natural-water` covers liquid surface response, and `simulate-natural-fog` covers clear writing and wiping on condensation. Preserve ice's faint accumulated friction marks rather than importing fog's clear erase behavior.

For the source map, numeric starting points, audio provenance, and known limitations, read [references/ice-study.md](references/ice-study.md). Those values are tuning examples, not universal physical constants.
