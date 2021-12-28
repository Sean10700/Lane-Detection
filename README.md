# Ultra-Fast-Lane-Detection

### This github code is basically based on https://github.com/cfzd/Ultra-Fast-Lane-Detection 
#### (named, Ultra-Fast-Lane-Detection.)
PyTorch implementation of the paper "[Ultra Fast Structure-aware Deep Lane Detection](https://arxiv.org/abs/2004.11757)".

The original github code doesn't provide real-time lane detection code.(Lane Detection with Webcam source or Video source)
This Code includes lane detection code for Web-cam and Video files.

## Demo 

<img src="https://user-images.githubusercontent.com/69523669/147495615-045c2f78-db17-437c-9f63-80d763c84b7c.gif" width="600px">

<img src="https://user-images.githubusercontent.com/69523669/147502612-9bd491c9-0742-4ea0-bfe8-37950d533ced.gif" width="600px">



## Youtube Video link
><a href="https://youtu.be/wQOL6idaHNY
>" target="_blank"><img src="https://img.youtube.com/vi/wQOL6idaHNY/0.jpg" 
>alt="Demo" width="240" height="180" border="10" /></a>



### Requirements
For running the code, the following environments are required. 
- Linux(Ubuntu 18.04)
- CUDA ver 10.2
- CuDNN 8.0.5
- Python 3.7 (Conda virtual environment) 
- OpenCV C++

(This code is only executed in above environment, depending on the computer environment, it maybe possible to run the code in other environments.(e.g. Windows OS))
For install, please see [INSTALL.md](./INSTALL.md)


### Youtube Code Review and How to Run Video [Korean]

><a href="https://www.youtube.com/watch?v=BDvIT49YA40
>" target="_blank"><img src="https://img.youtube.com/vi/BDvIT49YA40/0.jpg" 
>alt="Demo" width="240" height="180" border="10" /></a>


><a href="https://youtu.be/RgvjWEfOHpU
>" target="_blank"><img src="https://img.youtube.com/vi/RgvjWEfOHpU/0.jpg" 
>alt="Demo" width="240" height="180" border="10" /></a>


### Trained Weight Files

will update the google drive url here later


*****

## The following description is from the https://github.com/cfzd/Ultra-Fast-Lane-Detection 

>## Ultra-Fast-Lane-Detection
>PyTorch implementation of the paper "[Ultra Fast Structure-aware Deep Lane Detection](https://arxiv.org/abs/2004.11757)".
>
>\[June 28, 2021\] Updates: we will release an extended version, which improves **6.3** points of F1 on CULane with the ResNet-18 backbone compared with the ECCV version.
>
>Updates: Our paper has been accepted by ECCV2020.
>
>
>The evaluation code is modified from [SCNN](https://github.com/XingangPan/SCNN) and [Tusimple Benchmark](https://github.com/TuSimple/tusimple-benchmark).
>
>Caffe model and prototxt can be found [here](https://github.com/Jade999/caffe_lane_detection).
>
>## Demo 
><a href="http://www.youtube.com/watch?feature=player_embedded&v=lnFbAG3GBN4
>" target="_blank"><img src="http://img.youtube.com/vi/lnFbAG3GBN4/0.jpg" 
>alt="Demo" width="240" height="180" border="10" /></a>
>
>
># Install
>Please see [INSTALL.md](./INSTALL.md)
>
># Get started
>First of all, please modify `data_root` and `log_path` in your `configs/culane.py` or `configs/tusimple.py` config according to your environment. 
>- `data_root` is the path of your CULane dataset or Tusimple dataset. 
>- `log_path` is where tensorboard logs, trained models and code backup are stored. ***It should be placed outside of this project.***
>
>
>
>***
>
>For single gpu training, run
>```Shell
>python train.py configs/path_to_your_config
>```
>For multi-gpu training, run
>```Shell
>sh launch_training.sh
>```
>or
>```Shell
>python -m torch.distributed.launch --nproc_per_node=$NGPUS train.py configs/path_to_your_config
>```
>If there is no pretrained torchvision model, multi-gpu training may result in multiple downloading. You can first download the corresponding models manually, and then restart >the multi-gpu training.
>
>Since our code has auto backup function which will copy all codes to the `log_path` according to the gitignore, additional temp file might also be copied if it is not filtered >by gitignore, which may block the execution if the temp files are large. So you should keep the working directory clean.
>***
>
>Besides config style settings, we also support command line style one. You can override a setting like
>```Shell
>python train.py configs/path_to_your_config --batch_size 8
>```
>The ```batch_size``` will be set to 8 during training.
>
>***
>
>To visualize the log with tensorboard, run
>
>```Shell
>tensorboard --logdir log_path --bind_all
>```
>
>## Trained models
>We provide two trained Res-18 models on CULane and Tusimple.
>
>|  Dataset | Metric paper | Metric This repo | Avg FPS on GTX 1080Ti |    Model    |
>|:--------:|:------------:|:----------------:|:-------------------:|:-----------:|
>| Tusimple |     95.87    |       95.82      |         306         | [GoogleDrive](https://drive.google.com/file/d/1WCYyur5ZaWczH15ecmeDowrW30xcLrCn/view?>usp=sharing)/[BaiduDrive(code:bghd)](https://pan.baidu.com/s/1Fjm5yVq1JDpGjh4bdgdDLA) |
>|  CULane  |     68.4     |       69.7       |         324         | [GoogleDrive](https://drive.google.com/file/d/1zXBRTw50WOzvUp6XKsi8Zrk3MUC3uFuq/view?>usp=sharing)/[BaiduDrive(code:w9tw)](https://pan.baidu.com/s/19Ig0TrV8MfmFTyCvbSa4ag) |
>
>For evaluation, run
>```Shell
>mkdir tmp
># This a bad example, you should put the temp files outside the project.
>
>python test.py configs/culane.py --test_model path_to_culane_18.pth --test_work_dir ./tmp
>
>python test.py configs/tusimple.py --test_model path_to_tusimple_18.pth --test_work_dir ./tmp
>```
>
>Same as training, multi-gpu evaluation is also supported.
>
>## Visualization
>
>We provide a script to visualize the detection results. Run the following commands to visualize on the testing set of CULane and Tusimple.
>```Shell
>python demo.py configs/culane.py --test_model path_to_culane_18.pth
># or
>python demo.py configs/tusimple.py --test_model path_to_tusimple_18.pth
>```
>
>Since the testing set of Tusimple is not ordered, the visualized video might look bad and we **do not recommend** doing this.
>
>## Speed
>To test the runtime, please run
>```Shell
>python speed_simple.py  
># this will test the speed with a simple protocol and requires no additional dependencies
>
>python speed_real.py
># this will test the speed with real video or camera input
>```
>It will loop 100 times and calculate the average runtime and fps in your environment.
>
># Citation
>
>```BibTeX
>@InProceedings{qin2020ultra,
>author = {Qin, Zequn and Wang, Huanyu and Li, Xi},
>title = {Ultra Fast Structure-aware Deep Lane Detection},
>booktitle = {The European Conference on Computer Vision (ECCV)},
>year = {2020}
>}
>```

Feel free to ask 
skev10700@gmail.com
