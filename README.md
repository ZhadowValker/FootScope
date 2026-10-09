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
3. Tap the red button: countdown, 5 s stand still, then walk (voice prompts guide each step).
4. Review the video, retake if needed, go to the next view.
5. Results show annotated frames and measurements. Use **Save / print PDF report** to export.

## Notes

- Screening aid only, not a diagnosis. 2-D pose estimation from a single phone camera has limits.
- Place the phone at hip height, steady, with the whole body in view and good lighting.
