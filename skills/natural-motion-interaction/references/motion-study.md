# Natural Effects motion adapters

Source snapshot: October 10, 2026, commit `71a83b3`, the private Natural Effects source project. These adapters are separate implementations, not an already unified input library.

## Source map

- `src/gestures/hand.ts`: MediaPipe tracking, feature extraction, and landmark smoothing.
- `src/gestures/LandmarkSmoother.ts`: One Euro filtering per hand index; index keys alone do not establish stable identity.
- `src/gestures/FogCamera.ts`: exclusive fog actions, mirrored cover crop, interpolation, bounded prediction, and lifecycle callbacks.
- `src/gestures/PondTouch.ts`: per-pointer velocity and pair geometry for water.
- `src/gestures/BodyMotion.ts`: image-change energy and horizontal activity centroid.
- `src/gestures/GestureRouter.ts`: older layered scene arbitration; its gesture vocabulary differs from the fog preset.

## Fog preset starting values

The tracker is configured for up to two hands and 30 Hz inference. The rendering path chooses one hand, using proximity to the previous target after initial selection. This is a heuristic: hand crossings may still switch identity. Do not describe it as robust multi-hand contact tracking.

Pinch strength enters above 0.72 and sustains above 0.58. A fist or open-palm classification excludes writing. Open palm has priority and uses palm center rather than fingertip coordinates. Samples older than 150 ms are not used as visible contact.

Coordinates come from the tracker's mirrored features and are transformed through the same aspect-preserving cover crop as the background. Do not mirror them a second time. Interpolation uses `1 - exp(-dt * 65)`; prediction is limited to 12 ms and four screen pixels per axis. The tracker uses minCutoff 18 and beta 8 for this preset, unlike the smoother's general defaults of 1 and 0.007. Different input units, cadence, and filter stacks require retuning.

Action changes release the old path and reset interpolation state. Tracking loss resets gesture state. Async startup uses an epoch to discard obsolete camera initialization, and stop cancels inference/render callbacks and disposes the tracker.

## Touch and body adapters

PondTouch stores each contact independently. First contact velocity is zero; subsequent segment time has an eight-millisecond floor and component velocities are clamped to plus or minus two normalized units per second. Pair rotation is wrapped with `atan2(sin(delta), cos(delta))`, and pair distances and axes correct for screen aspect. This pair heuristic chooses another contact; it is not a general multi-body constraint solver.

BodyMotion downsamples to 64 by 48, samples at most every 50 ms, subtracts average luminance change, and thresholds absolute pixel differences. It estimates activity energy and a mirrored horizontal centroid. Moving cameras, local lighting changes, and unrelated moving objects can still trigger it. It is neither pose tracking nor optical flow.

## Adaptation checks

Before sharing an adapter across materials, define its units and ownership of mirroring, crop, smoothing, and contact IDs. Test crossing and reacquisition explicitly. The existing implementation provides patterns and known limits; do not assume every preset already supports the same actions or stable hand identities.

## Source availability

The source map refers to the Natural Effects application, which is maintained in a private repository (live app: https://naturaleffects.vercel.app/). Its code and media are not bundled here. Snapshot commit identifiers document provenance and may not be publicly available. If the source is unavailable, use the behavioral guidance and tuning examples without assuming access to those files.
