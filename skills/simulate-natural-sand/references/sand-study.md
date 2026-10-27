# Sand study record

## Implementation evidence

Source: the Natural Effects application’s `docs/SAND-SNOW-STUDY.md` (private repository; live app: https://naturaleffects.vercel.app/), consulted October 15, 2026. Application code and recordings are maintained separately; if you have access, inspect current source before copying parameters.

The documented prototype separates full-resolution WebGL grain from a bounded deformation grid. Warped wind ripples and broad height variation form the initial surface. Displacement and downhill relaxation conserve modeled volume. Dwell ramps load over roughly two seconds; faster movement unloads it. These are implementation choices, not universal material constants.

Documented checks include visible ridges and granular strokes, volume conservation calculations, and a production build. The camera test returned “Could not start video source”; live tracking accuracy was not established. Do not turn these checks into a claim of physical realism or a new user acceptance result.

## Reference provenance

The original study inspected [Sahara ripples](https://wibnet.nl/natuur/bodem/wat-zit-er-onder-het-zand-van-de-sahara) and [Michael Mellinger's Erg Chebbi photograph](https://www.flickr.com/photos/theworldismycanvas/3212006676). Photos informed appearance and were not redistributed. They do not validate settling dynamics.

Audio: [sand-on-sand pour by martinimeniscus](https://freesound.org/people/martinimeniscus/sounds/199332/), credited as CC0 in the source application's `public/audio/CREDITS.md`. The prototype loops a middle section around 8–15 seconds with a crossfade, low-pass filtering, and gain driven by speed and brush area. Preserve attribution and verify the source license when acquiring assets; no audio file is bundled here.
