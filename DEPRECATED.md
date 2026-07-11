# ⚠️ DEPRECATED — do not use

This branch was an experiment replacing the lightweight detector with
**OpenCV.js** (adaptive background subtraction + Canny edge-density, real
contour outline, silhouette-masked crops).

**Status: deprecated — not merged.** Detection quality was not good enough:
presence detection (item vs. empty) was inconsistent in real conditions, and
it wasn't worth the ~10 MB OpenCV.js download and added CPU cost.

➡️ Use **`main`** instead. This branch is kept for reference only and is not maintained.
