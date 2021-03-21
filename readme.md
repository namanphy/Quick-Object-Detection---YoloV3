# Quick Object Detection with YoloV3

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/194MYhJSLJ7okuNpCD3tr0VaZK-CrTRIh?usp=sharing)

We are here training and fine-tuning the YoloV3 model for our custom classes using transfer learning.

The complete code is present [here](https://github.com/namanphy/Quick-Object-Detection---YoloV3/blob/main/YoloV3) and 
all the instructions are with respect to this directory only.

## Quick Instructions
### For google colab

1. Clone this repo and paste in your google drive.

2. Do the steps mentioned below for setting up train and test data.

3. Download weights as mentioned below.

4. Run the given python [notebook](https://github.com/namanphy/Quick-Object-Detection---YoloV3/blob/main/YoloV3_pytorch.ipynb). 
(with path to your folder in google drive)

5. Voila! Check the output folder for results.


**Check out the final output video by clicking below icon**

[<img src="https://www.flaticon.com/svg/vstatic/svg/1384/1384060.svg?token=exp=1616266334~hmac=3cefbc5b24168ba5f02a7399f7007de6" width="60">](https://youtu.be/1k42E9Skmeg)


## Hyper parameters
- batch size: 16
- epochs: 60

## Data Preparation
The structure of the dataset required to train the model is present 
[here](https://github.com/namanphy/Quick-Object-Detection---YoloV3/blob/main/YoloV3/data/HardhatVestMaskBoots).

### Train Data

#### For the HardhatVestMaskBoots dataset

1. Download the dataset from [here](https://drive.google.com/file/d/1RlUgMtPfzzIdhB5zDgkXjL-v2UTjobme/view?usp=sharing)

2. Paste the contents of the `data.zip` in the data folder.

#### For your custom dataset

1. Collect the images for your dataset and annotate them using this tool present
in this [repo](https://github.com/miki998/YoloV3_Annotation_Tool).
2. Follow the instructions present in the mentioned repo to get the labels and images 
and other files as required.
3. Put your images in this [folder](https://github.com/namanphy/Quick-Object-Detection---YoloV3/blob/main/YoloV3/data/HardhatVestMaskBoots/images)
(some sample files are already there).
4. Put your labels in this [folder](https://github.com/namanphy/Quick-Object-Detection---YoloV3/blob/main/YoloV3/data/HardhatVestMaskBoots/images)
(some sample files are already there.
5. Make sure to check the `.data` file for correct paths.

### Test Data

For images or non-video data simply put your images in this [folder](https://github.com/namanphy/Quick-Object-Detection---YoloV3/blob/main/YoloV3/data/test).

Follow below steps for a video :

- Download a short video containing the classes used during training.
- Extract frames from the video into the [test](https://github.com/namanphy/Quick-Object-Detection---YoloV3/blob/main/YoloV3/data/test) directory

    `ffmpeg -i ../video.mp4 data/test/image-%3d.jpg`

- Also extract audio from the video - for later

    `! ffmpeg -i video.mp4 -f mp3 -ab 192000 -vn audio.mp3`


### Training

1. Download the weight file `yolov3-spp-ultralytics.pt` of pre-trained YoloV3 from [here](https://drive.google.com/open?id=1LezFG5g3BCW6iYaV89B2i64cqEUZD7e0) 
and paste it in the [weights](https://github.com/namanphy/Quick-Object-Detection---YoloV3/blob/main/YoloV3/weights) folder.
2. Train the model using the command mentioning batch size and epochs.

    `python train.py --data data/<data_filename>.data --batch 16 --cache --cfg cfg/yolov3-spp.cfg --epochs 60`

### Inference

Use this command to for inference on the files present in `data\test` folder.

`python detect.py --conf-thres 0.2 --output output`

#### On video dataset
After extracting frames from video and doing inference.

- Merge the output files into video.

    `ffmpeg -i output/image-%3d.jpg -framerate 24 output_video.mp4`

- Add the audio file onto the output video to produce the final video.

    `ffmpeg -i output_video.mp4 -i audio.mp3 -shortest final_video.mp4`

## Results

This is a sample result after training for 60 epochs.

![inference](https://github.com/namanphy/Quick-Object-Detection---YoloV3/blob/main/YoloV3/inference.jpg)
 