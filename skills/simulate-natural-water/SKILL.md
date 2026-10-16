---
name: simulate-natural-water
description: Build or refine interactive water surfaces with ripples, directional wakes, stirring, local compression, and reflection or refraction. Use for touch, pointer, or camera-driven water experiences, rather than generic particle animations.
---

# Simulate Natural Water

Translate contact into a coherent moving surface. Establish the intended scale and setting from the request: a quiet pond, shallow pool, stream, and ocean need different motion. The Natural Effects study is an artistic surface model, not a fluid dynamics solver.

## Surface response

- Separate entry ripples from continuous movement. A contact can launch a small outward wave; dragging produces a directional wake related to speed and direction. Avoid emitting identical rings on every frame or while stationary.
- Let motion carry beyond the contact and decay after release. Maintain independent contact state so a second finger never inherits the first finger's position or velocity.
- Stirring changes rotational motion; converging contacts can displace a local mound and surrounding trough. Do not substitute image scaling or camera zoom for water displacement.
- Keep calm background motion subordinate to interaction. Combine different spatial scales without a conspicuous repeated sine pattern. Evaluate the surface while idle as well as during motion.

## Appearance and implementation

Derive reflection or refraction from surface slopes, with restrained highlights and a consistent light direction. Match the appearance to the chosen depth and material context; avoid large elastic image distortions, bright fixed stripes, and glitter unrelated to the waves. A height-field shader is useful for this study; other models are appropriate when flow transport, boundaries, or volume matter.

Use elapsed seconds for propagation, damping, and integration. For linear damping, `exp(-rate * dt)` avoids frame-rate-dependent decay. Clamp or substep long integration gaps without slowing contact tracking. Correct for aspect ratio in distance calculations. Bound active contacts and retained wakes, and cap render resolution independently of input precision.

Camera reflections and audio response are optional. Keep image cropping and mirroring consistent with interaction coordinates. If sound is requested, make sound part of movement: contact size, speed, direction changes, and release should shape its response. Gesture-driven synthesis may use recorded source layers, filtering, envelopes, and event scheduling; describe the method accurately and retain source credits. A fingertip and broad hand can have different contact scales without arbitrarily changing pitch. Sustain sound through continuous lateral motion and fade naturally on stopping; avoid cooldowns that create silent gaps, repeated identical splashes, or sweeping tones. Audition against the intended setting: generic water audio may not read as a quiet pond. Resume audio on a user gesture and clean up on interruption.

## Verification

Compare a tap, stationary hold, slow drag, fast sweep, sharp turn, release, two independent contacts, and reset. Check portrait and landscape alignment and a long frame gap. A release should leave decaying surface motion without continued input emission. Inspect mobile frame pacing and graphics failure recovery. Report observed checks separately from physical realism or device-specific audio quality.

For source locations, useful starting values, and the current model's limits, read [references/water-study.md](references/water-study.md) when adapting the Natural Effects water study. Gesture adapters can be designed with `natural-motion-interaction` when available; this skill does not require it.
