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

### Day 4:
The next step is loading and visualizing the data.

**Loading:**

The 3DSceneGraph dataset is designed for 3D reconstruction of a scene making the data loader provided by the owner too complex for the needs of this project.

Information to neglect:
- all Gibson environment requirements,
- camera,
- building, and
- room.

Therefore, I will have to build my own data loader. The dataset consists of a `.npz` file for each building, so, [`numpy.load`](https://numpy.org/doc/stable/reference/generated/numpy.load.html#numpy.load) must be used to load data.

**Data visualization results:**

Each file contains the data corresponding to a building divided into a python dictionary with the following keys:

{'building', 'room', 'object', 'camera', 'panorama'}

We won't need the data for 'building', 'room' and 'camera'. The most important key is 'panorama' and will be used as it is. The data under the key 'object' contains all the data for each object with the following subkeys:

{'action_affordance', 'floor_area', 'surface_coverage', 'class_', 'id', 'location', 'material', 'size', 'tactile_texture', 'visual_texture', 'volume', 'parent_room'}


Here's a sample for the first object:

|**key**|arg|
|-------|:---:|
|**'action_affordance':**| ['bake', 'eat', 'dip', 'through away', 'bite'] |
|**'floor_area':**| 2.5151038780730564 |
|**'surface_coverage':**| 0.7226956182334275| 
|**'class_':**| 'cake' |
|**'id':**| 1 |
|**'location':**| array([-4.83867198,  2.90227134,  6.25435385]) |
|**'material':**| None |
|**'size':**| array([1.2509156 , 0.03512015, 0.62766802]) |
|**'tactile_texture':**| None |
|**'visual_texture':**| None |
|**'volume':**| 0.018281155256639165 |
|**'parent_room':**| 17|

### Day 5:

It turns out that the panoramic images in the dataset are the annotations, not the raw images. Gibson is needed to generate the 3D model of the building and give simulate the 360 pictures. I discarded using Gibson earlier in the process since I don't intend to build a reconstruction model. Now I need to use it to get the required data.