# Dataset

Introduce properties of Datasets.

## NYU Depth Dataset v2
[homepage](http://cs.nyu.edu/~silberman/datasets/nyu_depth_v2.html) <br>
(The following contents are from the NYU Depth Dataset v2 homepage) <br>

![im1](https://github.com/jinghongkyq/Dataset/raw/master/images/nyu_depth_v2_web.jpg)
![im2](https://github.com/jinghongkyq/Dataset/raw/master/images/nyu_depth_v2_web2.jpg) <br>
Samples of the RGB image, the raw depth image, and the class labels from the dataset. <br>

### Overview

The NYU-Depth V2 data set is comprised of video sequences from a variety of indoor scenes as recorded by both the RGB and Depth cameras from the Microsoft Kinect. It features: <br>

* 1449 densely labeled pairs of aligned RGB and depth images <br>
* 464 new scenes taken from 3 cities <br>
* 407,024 new unlabeled frames <br>
* Each object is labeled with a class and an instance number (cup1, cup2, cup3, etc) <br>

The dataset has several components: <br>

* Labeled: A subset of the video data accompanied by dense multi-class labels. This data has also been preprocessed to fill in missing depth labels. <br>
* Raw: The raw rgb, depth and accelerometer data as provided by the Kinect. <br>
* Toolbox: Useful functions for manipulating the data and labels. <br>

### Labeled dataset

![im3](https://github.com/jinghongkyq/Dataset/raw/master/images/nyu_depth_v2_labeled.jpg) <br>
Output from the RGB camera (left), preprocessed depth (center) and a set of labels (right) for the image. <br>

The labeled dataset is a subset of the Raw Dataset. It is comprised of pairs of RGB and Depth frames that have been synchronized and annotated with dense labels for every image. In addition to the projected depth maps, we have included a set of preprocessed depth maps whose missing values have been filled in using the colorization scheme of Levin et al. Unlike, the Raw dataset, the labeled dataset is provided as a Matlab .mat file with the following variables: <br>

* accelData – Nx4 matrix of accelerometer values indicated when each frame was taken. The columns contain the roll, yaw, pitch and tilt angle of the device. <br>
* depths – HxWxN matrix of in-painted depth maps where H and W are the height and width, respectively and N is the number of images. The values of the depth elements are in meters. <br>
* images – HxWx3xN matrix of RGB images where H and W are the height and width, respectively, and N is the number of images. <br>
* instances – HxWxN matrix of instance maps. Use get_instance_masks.m in the Toolbox to recover masks for each object instance in a scene. <br>
* labels – HxWxN matrix of object label masks where H and W are the height and width, respectively and N is the number of images. The labels range from 1..C where C is the total number of classes. If a pixel’s label value is 0, then that pixel is ‘unlabeled’.
* names – Cx1 cell array of the english names of each class. <br>
* namesToIds – map from english label names to class IDs (with C key-value pairs) <br>
* rawDepths – HxWxN matrix of raw depth maps where H and W are the height and width, respectively, and N is the number of images. These depth maps capture the depth images after they have been projected onto the RGB image plane but before the missing depth values have been filled in. Additionally, the depth non-linearity from the Kinect device has been removed and the values of each depth image are in meters. <br>
* rawDepthFilenames – Nx1 cell array of the filenames (in the Raw dataset) that were used for each of the depth images in the labeled dataset. <br>
* rawRgbFilenames – Nx1 cell array of the filenames (in the Raw dataset) that were used for each of the RGB images in the labeled dataset. <br>
* scenes – Nx1 cell array of the name of the scene from which each image was taken. <br>
* sceneTypes – Nx1 cell array of the scene type from which each image was taken. <br>

### Raw Dataset

![im4](https://github.com/jinghongkyq/Dataset/raw/master/images/nyu_depth_v2_raw.jpg) <br>
Output from the RGB camera (left) and depth camera (right). Missing values in the depth image are a result of (a) shadows caused by the disparity between the infrared emitter and camera or (b) random missing or spurious values caused by specular or low albedo surfaces. <br>

The raw dataset contains the raw image and accelerometer dumps from the kinect. The RGB and Depth camera sampling rate lies between 20 and 30 FPS (variable over time). While the frames are not synchronized, the timestamps for each of the RGB, depth and accelerometer files are included as part of each filename and can be synchronized to produce a continuous video using the get_synched_frames.m function in the Toolbox. <br>

The dataset is divided into different folders which correspond to each ’scene’ being filmed, such as ‘living_room_0012′ or ‘office_0014′. The file hierarchy is structured as follows: <br>

/ <br>
../bedroom_0001/ <br>
../bedroom_0001/a-1294886363.011060-3164794231.dump <br>
../bedroom_0001/a-1294886363.016801-3164794231.dump <br>
                  ... <br>
../bedroom_0001/d-1294886362.665769-3143255701.pgm <br>
../bedroom_0001/d-1294886362.793814-3151264321.pgm <br>
                  ... <br>
../bedroom_0001/r-1294886362.238178-3118787619.ppm <br>
../bedroom_0001/r-1294886362.814111-3152792506.ppm <br>

Files that begin with the prefix a- are the accelerometer dumps. These dumps are written to disk in binary and can be read with file get_accel_data.mex. Files that begin with the prefix r- and d- are the frames from the RGB and depth cameras, respectively. Since no preprocessing has been performed, the raw depth images must be projected onto the RGB coordinate space into order to align the images. <br>

### Toolbox

The matlab toolbox has several useful functions for handling the data. <br>

* camera_params.m - Contains the camera parameters for the Kinect used to capture the data. <br>
* crop_image.m – Crops an image to use only the area when the depth signal is projected. <br>
* fill_depth_colorization.m – Fills in the depth using Levin et al's Colorization method. <br>
* fill_depth_cross_bf.m - Fills in the depth using a cross-bilateral filter at multiple scales. <br>
* get_accel_data.m - Returns the accelerometer parameters at a specific moment in time. <br>
* get_instance_masks.m – Returns a set of binary masks, one for each object instance in an image. <br>
* get_rgb_depth_overlay.m – Returns a visualization of the RGB and Depth alignment. <br>
* get_synched_frames.m - Returns a set of synchronized RGB and Depth frames that can be used to produced RGBD videos of each scene. <br>
* get_timestamp_from_filename.m – Returns the timestamp from the raw dataset filenames. This is useful for sampling the RAW video dumps at even intervals in time. <br>
* project_depth_map.m – Projects the Depth map from the Kinect on the RGB image plane. <br>
