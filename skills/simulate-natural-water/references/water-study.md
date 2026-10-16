# Natural Effects water implementation reference

Source snapshot: October 10, 2026, commit `71a83b3` in the Natural Effects source project (`ambershen/dirty-window`). Locate equivalent files if moved and inspect the current implementation before copying values. Entry: `?mode=water` (routed to the water scene by the current fallback); `?mode=classic` is a separate older scene.

## Source map

- `src/effects/WaterSurface.ts`: WebGL height function, slope-based texture displacement, ripples, directional wakes, vortex, and compression spring.
- `src/gestures/PondTouch.ts`: independent pointer positions, velocity, pair rotation, compression, and aspect-corrected pair axis.
- `src/midnight.ts`: scene composition and input/audio integration.
- `src/audio/WaterSoundscape.ts` and `src/audio/WaterAudio.ts`: inspect before reusing audio; not every water mode uses the same path.
- `src/gestures/BodyMotion.ts`: coarse image-change energy, not pose or optical flow.

## Starting points, not physical constants

The shader retains eight ripple slots and sixteen current slots: eight contact currents and eight trailing wakes. Ripple emission is limited to one per 90 ms per contact and requires about 0.012 aspect-corrected normalized movement after the first sample. Ripple envelopes propagate at 0.24 normalized height units per second and decay with `exp(-age * 0.9)`.

Directional wake width and length grow with capped speed. Drag input speed is capped at two normalized units per second. Trailing samples are emitted at most once per 65 ms per contact; meaningful turns can add a small vortex. Released currents advect and decay rather than vanishing. Current damping rates are 1.4 for active slots and 0.85 for inactive slots; vortex strength decays at 0.8 per second.

Pair compression drives a spring: acceleration includes `-22 * displacement - 4 * velocity`. This is a local visual displacement model, not conserved fluid volume. The shader mound and surrounding trough approximate displaced water; no advection solver is present. Integration gaps are capped at 50 ms. Canvas longest dimension is capped at 1100 pixels.

## Limits and checks

The base waves are procedural, wakes have bounded history, and the vortex is a shared field. Do not describe this as independent interacting vortices or a solved river current. True transported foam, obstacle flow, and gravity-driven streams require additional state and validation.

Compare direction reversal and two-finger compression against ordinary dragging. Inspect for image zoom, rubbery stretching, periodic stripes, and jumps between pointers. Source existence and a successful build do not establish that the audio feels natural or every gesture is integrated in every scene.

## Source availability

The source map refers to [Natural Effects application](https://github.com/ambershen/dirty-window), a separate application. Its code and media are not bundled here. Snapshot commit identifiers document provenance and may not be publicly available. If the source is unavailable, use the behavioral guidance and tuning examples without assuming access to those files.
