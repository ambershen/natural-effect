# Natural Effects

A growing collection of skills for creating interactive natural materials and motion.

These skills capture material behavior, implementation patterns, sound mappings, and lessons from iteration. They guide a coding agent's decisions; they are not a rendering library or a physically validated simulation package.

The initial collection grew out of [States of Water](https://states-of-water-alpha.vercel.app/), an exploration of water, ice, and fog as interactive surfaces.

## Initial skills

| Skill | Focus |
| --- | --- |
| [simulate-natural-water](skills/simulate-natural-water/SKILL.md) | Ripples, directional wakes, stirring, inertia, reflection, and refraction. |
| [simulate-natural-ice](skills/simulate-natural-ice/SKILL.md) | Faint friction writing, irregular growing fractures, and restrained material sound. |
| [simulate-natural-fog](skills/simulate-natural-fog/SKILL.md) | Fogged glass, narrow writing, broad wiping, and gradual recovery. |
| [natural-motion-interaction](skills/natural-motion-interaction/SKILL.md) | Touch and camera input, contact lifecycles, gesture mapping, smoothing, and coordinate alignment. |

Material skills can be used independently. The motion skill provides shared input guidance while leaving each material free to respond differently.

## Use with Codex

Clone this repository and copy the desired folders from `skills/` into your Codex skills directory, normally `~/.codex/skills/` or `$CODEX_HOME/skills` when configured. Review existing folders before replacing a skill with the same name.

Once discovered by Codex, invoke a skill by name, for example:

```text
Use $simulate-natural-water to build a quiet water surface that responds to touch with directional wakes and decaying ripples.

Use $simulate-natural-fog with $natural-motion-interaction to create a fogged mirror: pinch to write, open palm to wipe, and release to stop.
```

## Structure

Each skill includes:

- `SKILL.md`: scope, material principles, workflow, and meaningful verification.
- `references/`: implementation notes, tuning examples, rejected approaches, and known limits.
- `agents/openai.yaml`: English discovery metadata and an example invocation.

All skill content is written in English. Numeric values describe particular studies rather than universal physical constants. Project-specific preferences are identified as such.

## Scope and source material

This repository contains skill instructions and reference notes. The original application code, tracking models, and audio assets are maintained separately in [States of Water](https://github.com/ambershen/dirty-window). Source maps identify project-relative paths; the skills remain usable when that implementation is unavailable.

Reference notes distinguish accepted behavior from experiments. Breath detection remains experimental, and source or build checks alone do not establish natural sound, reliable gesture recognition, or physical accuracy.

Future skills can extend the collection to other materials and phenomena as working experiments provide useful, reusable lessons.
