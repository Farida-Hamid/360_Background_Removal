Project Journal
---

**This file is to record the progress and problems faced while building this project.**

**In this journal you'll find:**
- Daily documenting for every day's work.
- Problems faced and how they were solved.
- Directions and decisions to follow or change paths.
- How I felt about each step.

### Day 1:
The first challenge was to find to decide what the project would be. I was looking for a Computer Vision challenge preferably background removal. After some research, I decided to work on a dataset of 360 images. So the research goal became to *find a semantic segmentation dataset of 360 images*.


### Day 2:
More research was needed to find such dataset. Luckily, not so many 360 datasets exist. Many of which are not for semantic segmentation purposes. Some not-so-bad choices were for depth estimation, one was built using a graphics generator instead of lively images, while others detected objects by drawing bounding boxes instead of pixel-wise detection.


### Day 3:
The datasets that made the cut needed deeper studying. The final decision was between [PASS](https://github.com/elnino9ykl/PASS), [ScanNet](http://www.scan-net.org/), [F-360iSOD](https://github.com/PanoAsh/F-360iSOD), and [3DSceneGraph](https://3dscenegraph.stanford.edu/database.html).

Street datasets are good options as self-driving cars propose difficult challenges on Computer Vision. Light variation and multiclass requirements make the challenge very interesting. However, since I have worked on street images in the past, I decided not to this time. Therefore I eliminated PASS.

Although F-360iSOD contains both indoor and outdoor scenes, it is much smaller than the remaining two. That is the case for most 360 datasets had they existed.

ScanNet and 3DSceneGraph are fairly large -at least compared to their competition-. They both offer many more features than needed for this project. I decided to download both datasets to either choose or merge them. turned out, 3DSceneGraph is more easily downloaded as ScanNet requires waiting for owners' permission.

The final decision on the dataset is 3DSceneGraph.

