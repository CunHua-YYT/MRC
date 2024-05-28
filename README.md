# MRC-PyTorch

##MRC test results
![Image](https://github.com/CunHua-YYT/MRC/blob/main/1_1Result/original(5729)_save.jpg)

### Requirements
- PyTorch>=1.0

You can install packages using pip according to [``requirements.txt``](./requirements.txt): 

```Shell
pip install -r requirements.txt
```

### Installation
1. Get the code. We will call the directory that you cloned into `$PRJ_ROOT`.
```Shell
git clone https://github.com/bo-zhang-cs/GAIC-Pytorch.git
```

2. Build the RoI&RoDAlign libraries. The source code of RoI&RoDAlign is from [[here]](https://github.com/lld533/Grid-Anchor-based-Image-Cropping-Pytorch) compatible with PyTorch 1.0 or later. If you use Pytorch 0.4.1, please refer to [[official implementation]](https://github.com/HuiZeng/Grid-Anchor-based-Image-Cropping-Pytorch).
```Shell
cd $PRJ_ROOT/untils
# Change the **CUDA_HOME** and **-arch=sm_86** in ``roi_align/make.sh`` and ``rod_align/make.sh`` according to your enviroment, respectively.
# Make sure these bash files (``make_all.sh, roi_align/make.sh, rod_align/make.sh``) are Unix text file format by runing ``:set ff=unix`` in VIM.
sudo bash make_all.sh
```

### Running Demo
1. Download pretrained models(~98MB) from [[Google Drive]](https://drive.google.com/file/d/1U_8C9oWOBT64LHtxZP1_0Uo9Ndw0QLsJ/view?usp=sharing) [[Baidu Cloud]](https://pan.baidu.com/s/1fmy18FD5_0v6vrab6OZKmQ)(access code: *webf*). By default, we assume the models (``*.pth``) is stored in `$PRJ_ROOT/pretrained_models`.

2. Predict best crops for the user's images.
```Shell
cd $PRJ_ROOT
python evaluate/demo.py --gpu 0 --image_dir $IMAGE_PATH/IMAGE_FOLDER --save_dir $RESULT_FOLDER
# or execute python evaluate/demo.py to predict best crops for the images in the test_images folder.
```

### Train/Evaluate
1. Download [GAICD dataset](https://github.com/HuiZeng/Grid-Anchor-based-Image-Cropping). And set the ``GAIC_folder`` in ``config.py`` and you can check the paths by running:
```Shell
cd $PRJ_ROOT
python dataset/cropping_dataset.py
```

2. Train your model and evaluate the model on the fly.
```Shell
cd $PRJ_ROOT
python train/train.py --gpu 0 --backbone vgg16
# or just running python train/train.py
```
The model performance for each epoch is also recorded in ``*.csv`` file under the produced ``experiments`` folder.
More model parameters and experimental settings can be found in ``config/GAIC_params.yaml``. 

3. Evaluate the pretrained model and reproduce the below quantitative results， the txt result will be saved.
```Shell
cd $PRJ_ROOT
python evaluate/test.py 
```


4.We placed the results of the 1:1 aspect ratio evaluation in the "txtResult" folder, and the visualizations of the top ten scores for the 1:1 aspect ratio in the "1_1Result" folder.

