# FootScope – posture & gait screening

Mobile-first web app for foot doctors. Records three guided videos (front, side, back), runs pose estimation (MediaPipe) in the browser, and reports knee alignment (knock-knee / bow-leg), heel/ankle, posture and gait measurements.

Everything runs on the phone. No video or data is uploaded.

## Host on GitHub Pages

1. Create a repository and upload `index.html` (and this README) to the root.
2. Repository **Settings → Pages → Build and deployment**: Source = *Deploy from a branch*, branch = `main`, folder = `/ (root)`.
3. Open `https://<your-user>.github.io/<repo>/` on your phone. The camera needs HTTPS, which GitHub Pages provides.

First load needs internet (pose model, about 10 MB, loaded from jsDelivr / Google storage).

## Checklist and flow

After the patient details, a checklist shows the three videos, four foot photos and five add-on tests with their status and a suggested next step. Do them in any order, redo any item, skip what you don't need, and open the report whenever something is done. Set-up steps fold away after you have seen them once for a view; the camera screen has a voice on/off button; the report has a section jump bar, a summary at the top and a Share summary button; leaving the page with unsaved results asks for confirmation.

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

## Cropping

- **Foot photos** (camera or gallery) open a crop screen first. A box is suggested automatically around the feet/legs; drag the corners (or the box) to adjust, or choose the whole photo. Marking then happens on the cropped picture.
- **Videos** (camera or gallery): the report pictures and walking frames are zoomed to the hips-to-feet area (the legs and heels), worked out from the tracked body. A checkbox on the review screen turns the zoom off. The saved video file itself stays full-frame.

## Looks (visual templates)

Tap **Look** on the home or results screen to switch the whole app between four designs. The choice is remembered on that phone; printed reports always use the plain Clinic layout.

- **Clinic**: bright and calm, teal accent, for daylight rooms.
- **Tape**: measuring-tape yellow and black, square and high contrast.
- **Radiograph**: dark blue-black with cyan lines and viewer-style corner marks, for dim rooms.
- **Pressure map**: deep indigo with a heat-map gradient accent.

Every screen shares one layout: a ruler-style progress rail, large touch targets, and a sticky bottom action bar for the main step.

## Notes

- Screening aid only, not a diagnosis. 2-D pose estimation from a single phone camera has limits.
- Place the phone at hip height, steady, with the whole body in view and good lighting.

## Studio (`studio.html`)

A single-page analysis view for walking video. Click a region of the foot and leg model (hip, knee, ankle, rearfoot, arch, forefoot) to see its measurements, the matching curves and the video frame where each value was measured, all without changing tabs.

- Loads a sample clip (side and front views in one frame) so it works straight away.
- **Upload video** or **Record video** runs pose detection in the browser (MediaPipe Pose Landmarker) and recomputes everything. Pick whether the clip is side, front, back, or side and front together.
- Measures knee, hip and ankle motion, stance and swing timing, cadence, step length and width, pelvic drop, trunk lean and sway, frontal knee alignment, and a rough rearfoot angle from a back view.
- Typical ranges are standard adult walking values from gait textbooks. Numbers come from one 2-D camera and are for screening, not diagnosis.
- **Separate recordings work.** Record or upload each view as its own clip. Every clip finds its own steps, so frontal knee alignment, step width and the rearfoot angle do not need a combined clip. Several walks of the same view are pooled into one average, so extra passes give steadier numbers. The first real clip replaces the sample.
- Results do not depend on where the person is in the frame or how large they appear, so walking across or towards the camera is fine.
- **Foot photo for the arch.** In the Arch panel, press Add foot photo, choose or take a side photo of a standing foot on an A4 sheet, and tap eight points (two ends of an A4 edge, heel, toe, ball, navicular, top of the foot, arch). Studio gives foot length, arch height index, navicular height and the gap under the arch, per foot, and adds them to the report. Photos stay on the device. **Auto-place points**: after tapping the heel and toe tip, it places the ball, navicular, top of the foot and arch point from the picture as hollow guesses; drag any point to correct it (every point can be dragged). The photo is taken at an angle, so treat the numbers as rough.
- **Back and front photos.** In the Rearfoot panel press Add back photo (rearfoot angle per heel, from the lower-leg line against the heel line) and in the Forefoot panel Add front photo (toe-out per foot, a rough figure because a front photo foreshortens the foot). Auto-place finds the jeans and bare feet and drops the points; drag any to correct.
- **Runtime analysis.** The big button on the dashboard opens the live camera with the skeleton, live joint angles, heel-strike rings, a step counter and every reading updating twice a second (side, front or back view), live curves, and the arch card. Press Record to save a pass; switching the view mid-recording starts a new pass. Moments (heel strikes, start, end, or by hand) are captured as pictures, readings are logged every second, and everything lands in the report (a Live session section with the timeline and the captured moments) while each pass becomes a normal clip for the region panels.
- **Gait patterns** panel checks nine common walking patterns (antalgic, Trendelenburg, waddling, steppage, Parkinsonian, hemiplegic, scissoring, sensory and cerebellar ataxic). Each lists the signs it looks for, what was measured, and whether they are present. The rules are simple rules of thumb for screening, not validated cut-offs and not a diagnosis. New measures behind them: toe clearance in swing, ankle angle in swing, arm swing, pelvic drop per standing leg, sideways foot swing, ankle crossing, and step-to-step variation.
- **Report** opens a printable one-page summary.
- Arch and foot posture still come from the close-up photo tool in `index.html`.
