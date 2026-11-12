---
license: cc-by-4.0
task_categories:
- keypoint-detection
tags:
- transparent-objects
- keypoints
- coco
- robotics
---

# GITW (Glasses-in-the-Wild), re-split for 2D-keypoints-benchmark

A repackaging of the [Glasses-in-the-Wild dataset](https://zenodo.org/records/17288503)
(DOI [10.5281/zenodo.17288503](https://doi.org/10.5281/zenodo.17288503)) for use in
[2D-keypoints-benchmark](https://github.com/tlpss/2D-keypoints-benchmark). The images and keypoint
annotations are unchanged; only the splits and some metadata differ.

1000 crowdsourced 256x256 images of transparent and partially filled drinking glasses, from 11
participants over 60 scenes and 93 unique glass types. Each image shows one annotated glass, with
5 keypoints: `bottom_front`, `top_left`, `top_right`, `top_front`, `fluid_level`.

## What was changed

1. **Splits.** The published validation split is used here as the **test** split, and a new
   validation split (10%, seed 2024) is carved out of the published train split, so that model
   selection never touches the reported test set.

   | split | images | source |
   |---|---|---|
   | train | 621 | 90% of the published train split |
   | val | 69 | 10% of the published train split |
   | test | 310 | the published validation split, unchanged |

2. **Bounding boxes added.** The published annotations contain keypoints only. An axis-aligned box
   around the labeled keypoints (padded by 10%, clipped to the image) was added to each annotation,
   because the YOLO conversion requires one. These boxes span the keypoints, not the full glass
   silhouette.

The upstream `annotations.xml` (a CVAT export) is **not** used: it refers to the original
pre-anonymisation file names and shares no file name with the shipped images. The `annotations.json`
inside each `images/` folder is the authoritative source and was used instead.

## Notes

Images are crops around a single glass, taken from photos that often contain several. Other glasses
are frequently visible inside a crop and are **not** annotated, so this data should not be used to
train or evaluate multi-instance detection.

## License and attribution

CC-BY-4.0, inherited from the original dataset. Please cite the original authors:
Louis Adriaens, Thomas Lips, Mathieu De Coster, Andreas Verleysen and Francis wyffels (Ghent University),
*Glasses-in-the-Wild Dataset*, 2025, DOI 10.5281/zenodo.17288503.
