---
name: simulate-natural-snow
description: Create or refine interactive powder snow, readable six-arm snowfall, dwell-based impressions, and gradual snow coverage. Use for snow surface artwork and touch or camera-driven snow simulations.
---

# Simulate Natural Snow

Build snow as a soft, opaque, densely layered material. Keep surface texture, airborne crystals, and deformation as separate systems that agree visually. This skill captures an artistically accepted browser study, not a physically validated snow model. Adapt its aesthetic to the user's request.

## Choose the relevant workflow

- For appearance or falling snow, read [references/snow-appearance.md](references/snow-appearance.md). Reusable original SVG snowflakes are in `assets/`.
- For pressing, drawing, settling, snowfall coverage, or input, read [references/snow-simulation.md](references/snow-simulation.md).

## Essential decisions

Favor a near-white matte base, dense fine crystals, and restrained cool crevices. Strong blue shadows, isolated outlined crystals, noisy embossed normals, and glints made this study look like ice. Preserve enough local shade to read an impression without tinting its interior blue.

Airborne snow must remain recognizable at the actual viewport size. In this study the user preferred visible six-arm branched SVG crystals over tiny aggregates. Treat that as an artistic legibility choice; do not imply all natural snow consists of large isolated symmetric crystals. Avoid bead-like circles with offset shadows.

Map holding longer to deeper compression unless hardware provides reliable pressure. Do not claim ordinary touch or a webcam measures force. Preserve existing responsive hand tracking when changing material appearance.

Use the application's existing renderer when practical. SVG, Canvas, WebGL, p5.js, Blender, or TouchDesigner are implementation choices, not required dependencies. Cache static crystal layers instead of drawing thousands of vectors each frame. A baked surface texture still needs to respond to compaction and fresh coverage.

## Verification and reporting

Check the untouched surface, fast trace, stationary hold, overlapping strokes, released contact, reset, snowfall on/off, and newly covered depressions. Compare held impressions at different frame rates. Confirm flakes have readable branches, subtle rotation, no dark water-drop halo, and no abrupt spawn or landing pop.

Inspect the running effect at phone and desktop sizes, including the actual shader compilation and texture loading. A TypeScript or bundler pass does not validate GLSL execution, appearance, frame rate, or camera accuracy. Report missing visual or physical-device checks explicitly. User approval is evidence of an accepted aesthetic, not scientific realism.

Keep skill content and reusable metadata in English. Do not bundle tracking models, unrelated application code, or third-party example source merely to save an implementation pattern.
