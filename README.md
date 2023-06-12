## enviroment requirement
* Python 3.6+
* PyTorch 1.3+
* CUDA 9.2+ (If you build PyTorch from source, CUDA 9.0 is also compatible)
* GCC 5+
* MMCV
### step 0. Create a conda virtual environment
```
conda create -n openmmlab python=3.8 -y
conda activate openmmlab
```

### step 1.Install Pytorch following official instruction
#### On GPU platforms(recommend):
```
pip3 install torch==1.10.2+cu113 torchvision==0.11.3+cu113 torchaudio==0.10.2+cu113 -f https://download.pytorch.org/whl/cu113/torch_stable.html
```

#### On CPU platforms:
```
conda install pytorch torchvision cpuonly -c pytorch
```

## Installation

### step 0. Install MMEngine, MMCV and MMDetection using MIM.
```
pip install -U openmim
mim install mmengine
mim install 'mmcv>=2.0.0rc4'
mim install 'mmdet>=3.0.0'
```

### step 1. Install MMDetection3D.
develop and run mmdet3d directly, install it from source(build from source):
```
git clone https://github.com/open-mmlab/mmdetection3d.git -b dev-1.x
or dowmload zip from ```https://github.com/open-mmlab/mmdetection3d/archive/refs/tags/v1.1.0.zip```
# "-b dev-1.x" means checkout to the `dev-1.x` branch.
cd mmdetection3d
pip install -v -e .
# "-v" means verbose, or more output
# "-e" means installing a project in edtiable mode,
# thus any local modifications made to the code will take effect without reinstallation.
```

## Verification
### Verify with point cloud demo 
To verify whether MMDetection3D is installed correctly, we provide some sample codes to run an inference demo.
* Step 1. We need to download config and checkpoint files.
```
mim download mmdet3d --config pointpillars_hv_secfpn_8xb6-160e_kitti-3d-car --dest .
```
The downloading will take several seconds or more, depending on your network environment. When it is done, you will find two files pointpillars_hv_secfpn_8xb6-160e_kitti-3d-car.py and hv_pointpillars_secfpn_6x8_160e_kitti-3d-car_20220331_134606-d42d15ed.pth in your current folder.

* Step 2. Verify the inference demo.
Case a: If you install MMDetection3D from source, just run the following command.
```
python demo/pcd_demo.py demo/data/kitti/000008.bin pointpillars_hv_secfpn_8xb6-160e_kitti-3d-car.py hv_pointpillars_secfpn_6x8_160e_kitti-3d-car_20220331_134606-d42d15ed.pth --show
```

for example:
```
cd ~/mmdetection3d/
python demo/pcd_demo.py demo/data/kitti/000008.bin pointpillars_hv_secfpn_8xb6-160e_kitti-3d-car.py hv_pointpillars_secfpn_6x8_160e_kitti-3d-car_20220331_134606-d42d15ed.pth --show


# use the parameter '--show' can get a visualized detection output
```
![demo](https://github.com/memory009/mmdetection3D/blob/main/figure/detect_000008.png)


### Pointcloud format Convert
CARLA outputs .ply by default as a point cloud result, so we should convert the output from '.ply' to '.bin' using ```format_convert.py``` 

### Detect 360° 
modify config.py
```
step1:
switch a config.py
e.g.pointpillars_hv_secfpn_8xb6-160e_kitti-3d-car.py
```

step2:

![figure_1](https://github.com/memory009/mmdetection3d-1.1.1/blob/main/figure/detect360.png)

