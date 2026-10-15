---
name: natural-motion-interaction
description: Map touch, pointer, tracked hand, or coarse body motion into responsive inputs for interactive materials. Use for contact lifecycles, pinch and palm gestures, coordinate alignment, motion smoothing, and material-specific action mapping.
---

# Natural Motion Interaction

Separate sensing from material response. Convert each input into a small set of meaningful contact and movement signals, then let the material decide how to react. A pinch can initiate writing on fog without implying that every material should draw the same line.

## Input contract

Use only signals needed by the experience. A useful conceptual contact contains an identity, timestamp, position with declared units, phase (`begin`, `move`, `end`, or `cancel`), velocity, contact radius, and action. Add confidence and load only if useful; label load's origin as reported pen pressure, dwell, or a gesture proxy. Camera landmarks and ordinary phone touch do not measure physical hand force.

Normalize coordinates at the adapter boundary. Apply the same crop, aspect correction, orientation, and mirroring as the rendered background, exactly once. Keep pixel brush radii distinct from normalized positions. Test alignment at the center and all four edges.

## Recognition and continuity

- Use hysteresis for thresholded gestures: stronger evidence enters contact, weaker evidence can sustain it. Define mutually exclusive actions and release the old contact before switching action.
- A useful fog mapping is pinch to write, release to idle, and an open palm to broad wiping. Treat this as a material-specific preset, not a universal gesture vocabulary.
- Track contacts independently. Array index is not a reliable hand identity when order changes; combine identity or handedness cues with continuity, reject implausible jumps, and reset when correspondence is uncertain. Prefer a new contact over connecting unrelated hands.
- On tracking loss, stale samples, pointer cancellation, focus loss, or teardown, end the contact and clear previous positions, filters, and velocity as needed. Reacquisition begins a new stroke.
- Decouple inference cadence from rendering. Process new samples once, interpolate at display cadence, and keep any short prediction spatially and temporally bounded. Never extrapolate a released or missing contact.

Use adaptive smoothing when jitter requires it: more smoothing for slow motion, less for fast motion. Tune from visible latency and measured jitter, not from a fixed preferred filter. Avoid stacking multiple filters that make the surface trail behind the hand. Use elapsed-time derivatives with consistent units and reset derivative history after interruptions.

## Material mapping

Water can use velocity, turn, and pair compression for wakes and stirring. Ice can accumulate friction from repeated slow movement and load from near-stationary dwell. Fog can use contact radius and trajectory for local clearing. Keep material state separate from gesture state: releasing input may stop emission while water continues moving or ice retains damage.

Coarse frame-difference motion can drive ambient energy, but it cannot establish body pose, hand identity, force, or a precise touch point. Document the measurement actually used. Keep camera processing local when that is the chosen design, and preserve explicit device controls and stop/retry behavior.

## Verification

Test idle hands, fast sweeps, slow tracing, threshold flutter, action changes, two hands crossing, one hand leaving, reacquisition, portrait/landscape resizing, and camera restart. Test multi-touch lift and cancel independently. Inspect accidental strokes, jump lines, duplicate processing, and runaway velocity after long gaps. Report untested hardware or recognition behavior plainly.

For concrete adapters and their limitations, read [references/motion-study.md](references/motion-study.md). Material skills such as `simulate-natural-water`, `simulate-natural-ice`, and `simulate-natural-fog` are optional companions.

## Reusable comparison inputs

Keep a short input study for tap, slow stroke, fast swipe, hold, two-finger compression, and release. Record timestamp units, viewport transform, device, and load source alongside the result. Use the same sequence across materials while allowing each material to ignore unsupported actions. A future replay fixture can compare revisions, but synthetic replay cannot validate camera recognition.
