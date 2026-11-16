# Animation Assignment — Three 3D Scenes

Three self-contained three.js animations, built as an animation-principles study.
Each file runs on its own: open it in any modern browser. Three.js r128 loads from a CDN.

| File | Scene | Length |
|---|---|---|
| `01-cat-and-mouse.html` | A cat watching a mouse circle around it | 8 s |
| `02-car-rotation.html` | A car rotating one full turn about its own vertical axis | 6 s |
| `03-conversation-crutches.html` | A legless man on crutches in a staged, dramatic conversation | 10 s |

## What each clip demonstrates

**01 — cat and mouse.** Anticipation (the mouse gathers itself, the cat coils before the
lunge), secondary action (head, eyes and whiskers tracking a moving target), squash and
stretch through the pounce, follow-through in the tail and ears, and an eased settle.
The mouse orbit and the cat's head turn are driven by separate timing curves, so the head
always lags the target by a beat.

**02 — car rotation.** Staging (a marked axis and a turntable give the rotation a
reference), slow-in / slow-out at both ends of the turn, constant angular velocity through
the middle, and overlapping action as the body rolls slightly behind the chassis.

**03 — conversation on crutches.** Staging (two figures, two lights, one dark stage),
expression carried by brows, mouth and posture, anticipation before each reply, and
exaggeration on the final line as the key light snaps tighter.

## Controls

Open the file and the animation plays and loops. Adding `#cap` to the URL switches the
page into frame-stepping mode, which is how the video versions were captured:

```js
window.__step(frameIndex)   // renders one deterministic frame
```

## Rebuilding the videos

The clips were captured frame by frame with puppeteer and encoded with ffmpeg:

```bash
node cap.js scene.html frames_dir 300                      # 300 frames at 1/30 s
ffmpeg -framerate 30 -i frames_dir/frame-%04d.png \
       -c:v libx264 -pix_fmt yuv420p -crf 19 out.mp4
```

## Notes

- Everything is procedural: no textures, no external models, no assets to load.
- Geometry is built from primitives (spheres, cylinders, cones) assembled into characters.
- Lighting, shadows and the caption overlays are part of the scene, not added in editing.
