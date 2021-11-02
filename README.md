# stereo_labeling

[![GitHub stars](https://img.shields.io/github/stars/Cartucho/stereo_labeling.svg?style=social&label=Stars)](https://github.com/Cartucho/stereo_labeling)


The goal of this tool is to label matches between the left and right images of a stereo video. I also added an interpolation feature so that you label only a few frame-pairs and then you press `i` (standing for interpolate) to automatically interpolate the labels for the other frame-pairs in between the ones that you labeled.

<img src="https://user-images.githubusercontent.com/15831541/139836761-24aeb645-61ef-47a4-9752-87411b5634e8.png">

On the bottom left of the interface you can see the current index of the image pair and the id of the currently selected keypoint. As I will explain, the idea is to label the keypoints one by one, from `id=0` until `id= number of keypoints that you will label`. I set the `w` `a` `s` `d` keys for navigating through the images and keypoint ids. By default `a` and `d` are used to go to the previous and next image, and `w` and `s` to go to the next and previous keypoint id. If you don't like these keys you can change them according to your preferance by editing the [config.yaml](https://github.com/Cartucho/stereo_labeling/blob/main/config.yaml) file. It is also in the [config.yaml](https://github.com/Cartucho/stereo_labeling/blob/main/config.yaml) file where you set the input directory, containing the images that you will label. I assume that you will have a folder with the left images, and another one with the right images.

## Usage

The usage idea is the following:
1. First choose the image keypoint that you will be labeling. You will label that keypoint on the entire video before starting to label the next keypoint;
2. After choosing the keypoint, go through the entire video, from index 0 onwards, and pay attention if the keypoint is visible in both the left and right images. If the keypoint is not visible in a specific image, press `v` (standing for `visibility`), which will toggle the `is_visible` between True and False. When `is_visible=False`, a red cross will show on top of the images to signal that the keypoint is not visible.
    + If you want to modify a range of pictures in once, press `r` (standing for range), then go select the range of images and click `v`, this way you toggle the visibility of all the selected pictures. The range is shown on the bottom left of the interface;
3. After marking all the pictures where the keypoint is not visible, you can start labeling the other pictures. You can do it by simply left-clicking over the keypoint in both the left and right image.
    + If you have `is_rectified: True` in the config file, then the interface will force you to choose the same height pixel coordinate for both the left and right image.
    + If you label a set of image pairs, for example if you label image_pair `0, 5, 10 and 15`, then if you press `i`, the images in between `1,2,...,4,6,7,...,9,11,...14` will be automatically labeled using interpolation. You can check the result of the interpolation if you don't like the result press `e` to eliminate a kpt label and then you can manually label that keypoint an press `i` again to refine the interpolation. You can only eliminate the currently selected keypoint id which is shown in red.
    + If you want to eliminate a range of pictures you can again use `r` for range, and select the image range first, followed by pressing `e` to eliminate;
4. Once you are satisfied with the labeling of that keypoint in the entire stereo video, you can go back to the img 0, press `w` to select the next keypoint id, and go back to step 1. to start labeling the next keypoint.

In summary, you want to (1) choose keypoint to be labeled, (2) mark visibility, (3) label, and repeat for the next keypoint.

Also, I suggest using a mouse since it will make the labeling process easier. You can even zoom in and out of the pictures using the middle scroll of the mouse.

## How to run it?

I recommend you to create a Python virtual environment:


```
python3.9 -m pip install --user virtualenv
python3.9 -m virtualenv venv
```

Then you can activate that environment and install the requirements using:
```
source venv/bin/activate
pip install -r requirements.txt
```

Now, when the `venv` is activated you can run the code using:

```
python main.py
```
