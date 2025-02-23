# Realtime Multi-Person Pose Estimation
By [Zhe Cao](https://people.eecs.berkeley.edu/~zhecao/), [Tomas Simon](http://www.cs.cmu.edu/~tsimon/), [Shih-En Wei](https://scholar.google.com/citations?user=sFQD3k4AAAAJ&hl=en), [Yaser Sheikh](http://www.cs.cmu.edu/~yaser/).

## Introduction
Code repo for winning 2016 MSCOCO Keypoints Challenge, 2016 ECCV Best Demo Award, and 2017 CVPR Oral paper.  

Watch our video result in [YouTube](https://www.youtube.com/watch?v=pW6nZXeWlGM&t=77s) or [our website](http://posefs1.perception.cs.cmu.edu/Users/ZheCao/humanpose.mp4). 

We present a bottom-up approach for realtime multi-person pose estimation, without using any person detector. For more details, refer to our [CVPR'17 paper](https://arxiv.org/abs/1611.08050), our [oral presentation video recording](https://www.youtube.com/watch?v=OgQLDEAjAZ8&list=PLvsYSxrlO0Cl4J_fgMhj2ElVmGR5UWKpB) at CVPR 2017 or our [presentation slides](http://image-net.org/challenges/talks/2016/Multi-person%20pose%20estimation-CMU.pdf) at ILSVRC and COCO workshop 2016.

<p align="left">
<img src="https://github.com/ZheC/Multi-Person-Pose-Estimation/blob/master/readme/dance.gif", width="720">
</p>

<p align="left">
<img src="https://github.com/ZheC/Multi-Person-Pose-Estimation/blob/master/readme/shake.gif", width="720">
</p>

This project is licensed under the terms of the [license](LICENSE).

## Other Implementations
Thank you all for the efforts! If you have new implementation and want to share with others, feel free to make a pull request or email me! 
- Our new C++ library [OpenPose](https://github.com/CMU-Perceptual-Computing-Lab/openpose) (testing only)
- Tensorflow [[version 1]](https://github.com/michalfaber/keras_Realtime_Multi-Person_Pose_Estimation) | [[version 2]](https://github.com/ildoonet/tf-openpose) | [[version 3]](https://github.com/raymon-tian/keras_Realtime_Multi-Person_Pose_Estimation)
- Pytorch [[version 1]](https://github.com/tensorboy/pytorch_Realtime_Multi-Person_Pose_Estimation) | [[version 2]](https://github.com/last-one/Pytorch_Realtime_Multi-Person_Pose_Estimation)
- Chainer [[version 1]](https://github.com/DeNA/Chainer_Realtime_Multi-Person_Pose_Estimation)
- MXnet [[version 1]](https://github.com/dragonfly90/mxnet_Realtime_Multi-Person_Pose_Estimation)
- MatConvnet [[version 1]](https://github.com/coocoky/matconvnet_Realtime_Multi-Person_Pose_Estimation)


## Contents
1. [Testing](#testing)
2. [Training](#training)
3. [Citation](#citation)

## Testing

### C++ (realtime version, for demo purpose)
- In May 2017, we released an updated library: [OpenPose](https://github.com/CMU-Perceptual-Computing-Lab/openpose)
- Old modified caffe version (not maintained anymore, please use OpenPose instead): [caffe_rtpose](https://github.com/CMU-Perceptual-Computing-Lab/caffe_demo/). Follow the instruction on that repo. 
- Three input options: images, video, webcam

### Matlab (slower, for COCO evaluation)
- Compatible with general [Caffe](http://caffe.berkeleyvision.org/). Compile matcaffe. 
- Run `cd testing; get_model.sh` to retrieve our latest MSCOCO model from our web server.
- Change the caffepath in the `config.m` and run `demo.m` for an example usage.

### Python
- `cd testing/python`
- `ipython notebook`
- Open `demo.ipynb` and execute the code
```
Alternative for experienced Python users: Installing Jupyter with pip
Important

Jupyter installation requires Python 3.3 or greater, or Python 2.7. IPython 1.x, which included the parts that later became Jupyter, was the last version to support Python 3.2 and 2.6.

As an existing Python user, you may wish to install Jupyter using Python’s package manager, pip, instead of Anaconda.

First, ensure that you have the latest pip; older versions may have trouble with some dependencies:

pip3 install --upgrade pip
Then install the Jupyter Notebook using:

pip3 install jupyter
(Use pip if using legacy Python 2.)

Congratulations. You have installed Jupyter Notebook. See Running the Notebook for more details.
https://jupyter.readthedocs.io/en/latest/install.html
```

## Training

### Network Architecture
![Teaser?](https://github.com/ZheC/Multi-Person-Pose-Estimation/blob/master/readme/arch.png)

### Training Steps 
- Run `cd training; bash getData.sh` to obtain the COCO images in `dataset/COCO/images/`, keypoints annotations in `dataset/COCO/annotations/` and [COCO official toolbox](https://github.com/pdollar/coco) in `dataset/COCO/coco/`. 
- Run `getANNO.m` in matlab to convert the annotation format from json to mat in `dataset/COCO/mat/`.
- Run `genCOCOMask.m` in matlab to obatin the mask images for unlabeled person. You can use 'parfor' in matlab to speed up the code.
- Run `genJSON('COCO')` to generate a json file in `dataset/COCO/json/` folder. The json files contain raw informations needed for training.
- Run `python genLMDB.py` to generate your LMDB. (You can also download our LMDB for the COCO dataset (189GB file) by: `bash get_lmdb.sh`)
- Download our modified caffe: [caffe_train](https://github.com/CMU-Perceptual-Computing-Lab/caffe_train). Compile pycaffe. It will be merged with caffe_rtpose (for testing) soon.
- Run `python setLayers.py --exp 1` to generate the prototxt and shell file for training.
- Download [VGG-19 model](https://gist.github.com/ksimonyan/3785162f95cd2d5fee77), we use it to initialize the first 10 layers for training.
- Run `bash train_pose.sh 0,1` (generated by setLayers.py) to start the training with two gpus. 

## Citation
Please cite the paper in your publications if it helps your research:

    
    
    @inproceedings{cao2017realtime,
      author = {Zhe Cao and Tomas Simon and Shih-En Wei and Yaser Sheikh},
      booktitle = {CVPR},
      title = {Realtime Multi-Person 2D Pose Estimation using Part Affinity Fields},
      year = {2017}
      }
	  
    @inproceedings{wei2016cpm,
      author = {Shih-En Wei and Varun Ramakrishna and Takeo Kanade and Yaser Sheikh},
      booktitle = {CVPR},
      title = {Convolutional pose machines},
      year = {2016}
      }
