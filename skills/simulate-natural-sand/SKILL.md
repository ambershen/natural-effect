---
name: simulate-natural-sand
description: Build or refine interactive sand surfaces with granular texture, furrows, displaced rims, downhill settling, and movement-driven sound. Use for touch or gesture drawing in sand and temporary canvas studies.
---

# Simulate Natural Sand

Translate a finger moving through loose grains into a changing surface. Establish the intended material first: dry loose sand, damp compact sand, and submerged sand need different responses. The documented prototype models dry sand artistically, not a validated granular solver.

## Observe and decompose

Study ridge direction, grain scale, furrow edges, displacement, and what remains after a hand leaves. Separate what a still photograph shows from movement inferred from video or direct observation. See [the study record](references/sand-study.md) for provenance and limits.

## Behavior and expressive controls

- Keep fine grain shading independent of the bounded height grid so resolution changes do not turn grains into large lumps.
- A fingertip creates a narrow furrow; a broad contact moves a wider patch. Redistribute displaced height to nearby rims rather than painting a dark stroke.
- Relax steep slopes downhill using elapsed time. Preserve displaced volume within the modeled domain, or explicitly account for material leaving its boundary.
- Let repeated passes alter existing ridges. Holding can increase modeled load, while fast motion unloads; label dwell and gesture load as proxies, not measured hand pressure.
- Keep settled marks after release. Introduce wind or fresh deposition only when requested; an automatic opacity fade does not describe grains moving.

Tune brush width, displacement, slope threshold, settling rate, and grain contrast separately. Keep input responsive even when the material resists movement. Avoid overly regular ridges, rubber-like stretching, bright pen lines, or constant particle spray.

## Sound mapping

Use a credited grain recording when appropriate, then shape playback with movement speed and contact area. A quiet continuous section with a crossfaded seam can support sustained movement; fade to silence on stopping. Avoid triggering a new pour on every input frame. Unlock audio during a user gesture, support mute, and clean up on interruption. Listening is needed to judge whether the sound matches the scale of the gesture.

## Verify

Compare tap, slow stroke, fast swipe, hold, two-contact compression, and release. Compression is a deliberate mapping to define, not an automatically supported pinch gesture. Check overlapping strokes, rim settling, volume accounting, frame-rate consistency, reset, and phone orientation. Check audio startup and continuous movement on the target device. Report visual, listening, and camera checks separately from build success.
