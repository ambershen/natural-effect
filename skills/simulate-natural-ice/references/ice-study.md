# Ice study implementation reference

Captured from the user-accepted direction in the dirty-window project, October 9, 2026. The user accepted the overall direction after friction writing was added. This records a reusable approach, not a claim of photorealism or confirmed audio quality on every device.

## Source map

Source project: [Natural Effects application](https://github.com/ambershen/dirty-window). Paths below are relative to that project, whose application code is not bundled with this skill. Inspect the available implementation before copying parameters.

- `src/ice.ts`: pointer contacts, load accumulation, render composition, reset, audio controls.
- `src/effects/IceWriting.ts`: half-resolution friction mask and muted underwater light.
- `src/effects/IceFractures.ts`: clipped Voronoi plates, shared jagged edges, growing contact branches and seam opening.
- `src/audio/IceSound.ts`: real recording playback, per-contact load events, rubbing envelopes, mute and iOS unlock.
- `src/ice.css`: fullscreen surface and icon controls.
- `public/audio/CREDITS.md`: source/licensing records.
- `docs/ICE-STUDY.md`: iteration history; older sections may describe superseded behavior.

Entry `?mode=ice`; root entry offers Water / Ice / Steam. Do not store temporary Cloudflare URLs as permanent skill links or imply a preview is deployed permanently.

## Friction writing starting points

All distances below are CSS pixels and speeds are pixels/second.

- Sample each stroke spatially, approximately every 2.5 px, independent of pointer event frequency.
- Contribution per sample: `clamp(13 / (speed + 35), 0.005, 0.19)`.
- Modulate contribution and brush radius with stable spatial grain. Current grain is `0.48 + 0.24*sin(x*0.071+y*0.049) + 0.18*sin(y*0.137-x*0.089)`; radius is `5.5 + grain*4`.
- Feathered radial stamps accumulate in a half-resolution mask. Repeated passes add clarity, while fast strokes stay nearly invisible.
- Render muted gray-green underwater light through the mask with final opacity capped at 0.25. This is an approximation of translucency; the layer is not actual water refraction.
- Refrost with exponential decay: remove `1-exp(-dt*0.075)` of mask opacity each frame; half-life approximately 9.2 seconds. Avoid frame-count-based fading.
- Writing does not wipe out the fracture network. Keep contact reflection soft and local.

The implemented pointer handler caps the elapsed segment time at 0.15 seconds to prevent a delayed event producing an oversized contribution. Do not use this cap to delay pointer tracking.

## Pressure and cracks

Current stationary test: no move event for 180ms, or speed below 8 px/s. Load increases with elapsed time, capped at 4, and decreases with movement. Treat this threshold as a heuristic; noisy or slow inputs may need tuning. Touch dwell is a proxy for force; only pen input currently supplements it with reported pressure.

The fracture engine uses shared recursively perturbed Voronoi edges, width variation, pale lips, and darker seams. Per-contact paths radiate at irregular angles with delayed branches. Growing load widens nearby edges over an expanding radius; adjacent plates settle according to edge opening. This is a stylized geometric response, not an elasticity solver. Released damage remains, bounded to 24 stored contact clusters. Reset rebuilds the plate network.

Static frost is cached; main canvas DPR is capped at 1.5. Keep brush accumulation and retained damage bounded when extending the system.

## Sound provenance and scheduling

These are Joseph SARDIN recordings from BigSoundBank, verified as CC0 when added. Recheck the source metadata if replacing or redistributing new assets.

| Local asset | Source | Material |
|---|---|---|
| `ice-rub.mp3` | https://bigsoundbank.com/defrost-1-s2219.html | Windshield frost rubbed by hand |
| `ice-crack.mp3` | https://bigsoundbank.com/cracking-ice-3-s2207.html | Real block of ice crushed in studio |
| `ice-crack-soft.mp3` | https://bigsoundbank.com/glace-qui-craque-1-s2205.html | Alternate real ice cracking take |

The file name “soft” identifies the alternate take; softness also comes from gain/filter settings. None is a verified recording of a bare finger pressing a frozen pond. They are material-recording approximations chosen for this interaction.

Current restrained mix:

- Master gain 0.48.
- Rubbing: single take up to 2.25s, at least 2.4s between starts; low-pass 1200Hz; gain `min(0.075, speed/8500)`, ~90ms smoothing. Motion inactivity over 70ms fades with a 55ms time constant. Stereo pan limited to ±0.3.
- Cracks: at most two load-threshold events per contact. First threshold 0.65–1.0, second 2.5–3.2; global cooldown 850ms; alternate two takes, play recorded tails. Gains 0.11 / 0.23; low-pass 2600 / 4300Hz; narrow stereo pan.
- AudioContext is created/resumed in pointerdown and resumed again on pointerup for mobile reliability; a one-sample silent buffer primes playback. Use `navigator.audioSession.type='playback'` where available. Fetch/decode asynchronously, with retry state on failure.
- Quiet/reset clears sources and contact counters. Release clears the per-pointer fracture counter. Cap simultaneous voices.

## Rejected approaches and lessons

- Blue ice: user chose gray-white.
- Smooth flat pane with thin straight lines: use frost grain and irregular connected plate boundaries.
- Bright white writing or flying particles on every glide: use subtle wet translucency from accumulated rubbing.
- Clear writing like fogged glass: enforce a low visibility ceiling; repeated effort improves only slightly.
- Slow writing triggering cracks: separate motion from stationary load.
- Frequent chopped rubbing and the same crack replayed on a timer: even real samples sound fake this way. Use continuity, sparse material events, and silence.
- Synthetic sweeping/watery tones: inappropriate for this accepted ice direction.

## Verification limits

The session checked builds, browser interactions, audio decode/readiness, mute, and bounded fracture triggers. A focused calculation confirmed slower strokes contribute more than fast strokes. The user's final response accepted the overall direction; detailed phone listening and tactile calibration still depend on their device. Never turn those limited checks into a claim of physical accuracy or universal iPhone verification.
