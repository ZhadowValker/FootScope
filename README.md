# FootScope – posture & gait screening

Mobile-first web app for foot doctors. Records three guided videos (front, side, back), runs pose estimation (MediaPipe) in the browser, and reports knee alignment (knock-knee / bow-leg), heel/ankle, posture and gait measurements.

Everything runs on the phone. No video or data is uploaded.

## Host on GitHub Pages

1. Create a repository and upload `index.html` (and this README) to the root.
2. Repository **Settings → Pages → Build and deployment**: Source = *Deploy from a branch*, branch = `main`, folder = `/ (root)`.
3. Open `https://<your-user>.github.io/<repo>/` on your phone. The camera needs HTTPS, which GitHub Pages provides.

First load needs internet (pose model, about 10 MB, loaded from jsDelivr / Google storage).

## How a session works

1. Enter patient name, age and height (height gives centimetre values).
2. For each view (Front, Side, Back) the app shows the phone and patient position, then opens the camera.
3. Tap the red button. The app tells you (on screen and by voice) to move away from the camera until the whole body fits the frame, then says "Ready. Recording in 5, 4, 3, 2, 1", then 5 s stand still, then walk.
   Or tap **Choose video from gallery** to analyse an existing video (it should start with about 5 s standing still, then the walk).
4. Review the video, retake if needed, go to the next view.
5. Results show annotated frames and measurements. Use **Save / print PDF report** to export.

## Report and printing

The results page has a **Save / print PDF report** button. It opens the phone's print dialog; choose **Save as PDF** (or a printer). The print layout is A4, white, with the patient header, one page per view (annotated frame, readings and six walking key frames with left leg in cyan and right leg in orange), then the foot close-ups and FPI pages, and an Examiner / Signature / Date line at the end.

## Camera screen aids

- **Level line + tilt message:** uses the phone's tilt sensor. Green means the phone is straight; the tilt is saved in the report. (iPhone asks for motion permission once.)
- **∠ button:** shows live joint angles on the skeleton (knees, heels, pelvis and shoulders from front/back; head, trunk, knee and ankle from the side).
- **Height:** enter feet & inches or cm; it converts automatically.

## Foot close-ups & Foot Posture Index

After the three walking videos the app asks for four photos (each can be skipped; camera or gallery):

1. **Heels from behind** – accurate heel (rearfoot) valgus/varus angle.
2. **Left foot, inner side** and 3. **Right foot, inner side** – medial arch angle (MLAA) and navicular height ÷ foot length.
4. **Both feet from above** – big-toe (hallux valgus) angle and foot toe-out/toe-in angle.

Each photo has a short picture guide. Tap the photo to place numbered landmarks (a magnifier shows the spot under your finger; drag to adjust). The angles are computed from your marks and drawn on the photo.

The report also has a **Foot Posture Index (FPI-6)** card for pronation / supination. Items 3 (heel position) and 5 (arch) are suggested from the photos; the clinician scores the other items and can change any of them. Total −12…+12: ≥10 highly pronated, 6–9 pronated, 0–5 normal, −1…−4 supinated, ≤−5 highly supinated.

Photo-based angles are estimates and depend on landmark placement; reference ranges are approximate. X-ray remains the standard for hallux valgus.

## Real-size scale and auto-suggested points

- On the marking screen, open **Reference object** and pick A4 paper, a bank card, a 10 cm ruler or a custom length. Tap its two ends on the photo. Foot length, navicular height and heel-to-heel distance are then also reported in cm. The object must lie in the same plane as the foot (flat on the floor beside it); tilt or height differences make the scale wrong.
- **Auto-suggest points** (toggle, off by default) separates the foot from the background by colour and suggests only points that can be read from the outline: heel and toe tip (and, with a reference object, the Achilles centre 10 cm above the floor in the heel photo). Suggestions are faded; joint points (ankle bone, navicular, big-toe joint) are never guessed. The report notes how many suggested points were kept. Works best on a plain floor or a sheet of white paper.

## More tests (balance, sit-to-stand, stairs, running)

Optional recordings from the home screen or the results screen, using the same framing check, countdown, voice and gallery-video option:

- **Balance on one leg** (left and right, 15 s, front-facing): time held, side-to-side sway, sway speed, pelvic drop on the lifted side, trunk lean; left vs right comparison.
- **Sit-to-stand (5 times)** (side view): stands counted, time for 5 stands against published reference values, rise time, slowing, knee extension, trunk lean.
- **Stairs** (side view): direction, step rate, step-time symmetry, knee bend, trunk lean.
- **Running** (side view, over-ground or treadmill): cadence, bounce, trunk lean, foot placement ahead of the hips, knee bend, foot strike, symmetry.

These are screening measures from 2-D phone video; sway, bounce and running values have no validated cut-offs for this method, so they are shown for comparison (left vs right, before vs after) rather than as pass/fail.

## Notes

- Screening aid only, not a diagnosis. 2-D pose estimation from a single phone camera has limits.
- Place the phone at hip height, steady, with the whole body in view and good lighting.
