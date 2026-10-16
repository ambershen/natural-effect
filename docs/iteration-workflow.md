# Updating a material skill

Use a short evidence loop: observe → describe → implement → compare → record.

## 1. Keep three kinds of evidence separate

- **Real-world reference:** source, material conditions, action, and what is actually visible or audible. A still image cannot establish timing or force.
- **Accepted prototype:** version or commit, demo, device, and the specific user feedback it satisfies. Aesthetic acceptance does not validate physics.
- **Experiment:** hypothesis, changed variable, observed result, and unresolved question. Keep it outside accepted defaults until reviewed.

Descriptions, images, and videos help an AI extract candidate rules. Treat those rules as hypotheses to inspect and tune, not measurements learned automatically from a reference.

## 2. Reuse one comparison sequence

Tap → slow stroke → fast swipe → stationary hold → two-finger compression → release. For each, record input, visible change, sound, and remaining state. Mark unsupported gestures rather than inventing behavior. Repeat relevant checks after resize, cancellation, and at different frame rates.

Keep short before/after clips with matching input and framing. A future recorded-input replay harness could make comparisons more repeatable; this repository does not implement one.

## 3. Promote a useful lesson

Update the smallest relevant layer: input continuity in the motion skill, response in the material skill, or expressive combinations in a recipe. Record why an approach failed as well as the replacement. Add numeric defaults only with units and context. Keep source code, skill guidance, and recipe settings distinguishable.

A compact entry:

```text
Material / version:
Reference and conditions:
Hypothesis / one changed variable:
Input and device:
Observed visual and sound response:
User feedback / acceptance scope:
Rejected approach and reason:
Untested behavior / next comparison:
```

## Current open comparisons

- Camera responsiveness: assess live tracking latency and jitter on target hardware; source checks cannot establish smoothness.
- Condensation: preserve the documented no-droplet default; any renewed droplet experiment needs separate evaluation of local recovery and timing.
- Sound: audition movement transitions and interruption/resume on the intended phone; decoded buffers do not establish naturalness.
- Projection: test scale, calibration, and full-body mappings as future experiments, not established capabilities of these skills.

## Per-material comparisons to record

- **Ice:** record glide, repeated rubbing, and sustained load separately, including the audible response. Keep the accepted gray-white appearance and faint writing distinct from proposed fracture tuning.
- **Fog:** compare a complete word or heart through its whole recovery; record release time, first visible recovery, and final disappearance.
- **Snow:** compare a moving trace with a held contact and inspect what remains after release. Keep the powder appearance separate from new sound experiments.

## Writing or restructuring a skill

Keep every `SKILL.md` in this order, leaving out sections that do not apply:

1. Frontmatter: `name` (lowercase, hyphenated, matching the folder) and a `description` that says what the skill builds and when to use it.
2. Intro: what the material is and what the model is not.
3. Material and interaction.
4. Appearance.
5. Sound.
6. Verification.
7. Study preset (Natural Effects): the original study's aesthetic choices, labelled so they can be told apart from general guidance.
8. Related skills and references.

Write instructions for the agent using the skill. Notes about maintaining this repository belong in this document instead. Keep skill content and metadata in English. Do not bundle tracking models, unrelated application code, third-party example source, or audio files; link to sources and credit them.
