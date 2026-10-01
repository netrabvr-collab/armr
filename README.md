# ARMR Assignment 1 – Marker-based WebAR demo

Image-tracking WebAR (MindAR 1.2.5 + A-Frame 1.5.0) that anchors a Draco-compressed `.glb` supercar on an image target.
Works in mobile Chrome (Android) **and** Safari (iOS) because it uses camera + WebGL, not the WebXR Device API.

## Files
| Path | Purpose |
|---|---|
| `index.html` | Scene, tracking, model post-processing, FPS/tracking HUD |
| `models/ARMR_Assign1.glb` | Optimised model (Part B output) |
| `assets/targets.mind` | Compiled MindAR target (sample card image) |
| `assets/target.png` | The image the camera must see |

## Deploy on GitHub Pages
1. Create a public repo, push everything in this folder to `main`.
2. Repo → **Settings → Pages → Deploy from a branch → main / (root)** → Save.
3. Open `https://<username>.github.io/<repo>/` on a phone (HTTPS is required for camera access).
4. Allow the camera, then point it at `assets/target.png` (shown on another screen or printed).

Local test: `python3 -m http.server 8000`, then use `ngrok`/`cloudflared` for an HTTPS URL on your phone.

## Use your own target image
1. Open https://hiukim.github.io/mind-ar-js-doc/tools/compile, upload a high-contrast, detail-rich image, click **Start**, download `targets.mind`.
2. Replace `assets/targets.mind` (and `assets/target.png` with your image).

## Tuning (top of the `<script>` in `index.html`)
- `FOOTPRINT` – car size relative to target width.
- `HIDE_EXTRA` – the exported .glb has **two copies** of the car; only the first is shown. Set `false` to show both.
- `DROP_TRANSMISSION` – disables the costly transmission pass.
- Tracking smoothness: `filterMinCF` (lower = smoother) and `filterBeta` (lower = less jitter, more lag) in the `mindar-image` attribute.

## Recording Part C results
The HUD (top-left) shows model status, tracking state and live FPS. Note FPS at 30 cm and 60 cm distance, at an angle, and with partial occlusion for each test phone.
