# Snow interaction and simulation

## State and input

Keep separate arrays for base height, current height, compaction, and disturbance. Render fine grain independently from the coarser height simulation. The study capped the simulation's longest edge at 560 cells.

Track each contact independently: position, radius, dwell load, last movement, last observation, and optional pen pressure. Begin with a shallow imprint; accumulate load while nearly stationary. The study started at 0.08 load, increased by 0.5 per second to a maximum of 1, and unloaded when movement exceeded about 25 CSS pixels/second. Allow small camera jitter without repeatedly resetting dwell. Pen pressure may supplement the proxy.

Interpolate stamps along moving paths. For sustained holds, use time-based integration such as `1 - exp(-14 * dt)`, rather than a fixed per-frame stamp amount. Release on pointer cancellation, lost capture, focus loss, stale camera observations, and gesture changes. The optional `natural-motion-interaction` skill provides more input guidance.

## Compression and gravity

Use a smooth radial depression with a slightly irregular boundary. Example depth was `0.14 + 0.96 * load`, with radius growing by up to 22 percent at full load. Increase compaction only where material is removed.

Snow compression reduces bulk volume. The study redistributed about 28 percent of removed height into a loose nearby rim; it deliberately did not conserve snow volume like dry sand. Do not describe this height-field heuristic as a full mass-density model.

Apply bounded local downhill transfers only above a repose threshold. Transfers between neighbors should conserve their sum and avoid directional bias by alternating traversal. Use stable time steps and bounded settling time. Verify settling separately from compression: compression intentionally removes bulk volume, downhill redistribution should not.

## Snowfall and coverage

A top-down surface view needs an altitude variable; screen Y alone does not describe contact with the ground. Lower altitude over time while adding slow lateral drift and rotation. At altitude zero, deposit into the surface at the landing position, then respawn overhead with a fade-in. Offscreen particles should not deposit at arbitrary clamped edge positions.

For the study's temporary canvas, snowfall gradually restored depressions toward the base and reduced compaction. An exponential rate around 0.075 per second was used alongside small local landing deposits. This is an artistic reset-through-snowfall effect, not physically accumulating snow depth. For true accumulation, add deposited mass and raise the reference surface instead of restoring to the original base.

Turning snowfall off must stop particles and coverage. Reset restores base heights and clears compression and disturbance. Keep continuous deposition capable of triggering rendering even when no hand is moving.

## Meaningful checks and known limits

Compare a brief touch with a stationary hold; the hold should deepen progressively and then saturate. Run equivalent holds at 30 and 60 fps. Confirm local settling conserves transferred height, snowfall fills existing impressions, and reset restores the original state.

The source study passed type/build and numerical behavior checks. Earlier browser checks exercised impressions and falling particles; later texture revisions were accepted by the user. Physical webcam tracking was not independently verified because the browser could not start the camera. Do not inherit a claim of verified tracking or mobile performance from this skill.

Source map: `src/effects/SnowSurface.ts`, the shared `src/effects/SandSurface.ts`, `src/sand.ts`, and `src/gestures/MaterialCamera.ts` in the original application.
