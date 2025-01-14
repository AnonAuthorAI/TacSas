# SGM Image Model
The SGM model for the image segmentation is obtained by fine-tuning the [Geospatial Foundation Model](https://huggingface.co/ibm-nasa-geospatial/Prithvi-100M/tree/main), whose encoder and decoder are based on vision transformers. We upload the fine-tuned model in the [anonymous folder](https://drive.google.com/drive/folders/1XvPIPN6vtS3M0oYwCui4VVVHPHlwDMG3?usp=sharing).

## Finetune the model
- Configure the paths in configs/multi_temporal_crop_classification.py
  ```
  cd ./configs
  ```
- Change the path in Lines 20, 55, and 63.
- Run the following command to train the model
  ```
  mim train mmsegmentation configs/multi_temporal_crop_classification.py
  ```

  Multi-gpu training can be run by adding `--launcher pytorch --gpus <number of gpus>`

## Environment setup
We follow the instruction of [NASA IMPACT](https://github.com/NASA-IMPACT/hls-foundation-os/) to setup the environment to segment the satellite.

### Setup
### Dependencies
1. Clone this repository
2. `conda create -n <environment-name> python==3.9`
3. `conda activate <environment-name>`
4. Install torch (tested for >=1.7.1 and <=1.11.0) and torchvision (tested for >=0.8.2 and <=0.12). May vary with your system. Please check at: https://pytorch.org/get-started/previous-versions/.
    1. e.g.: `pip install torch==1.11.0+cu115 torchvision==0.12.0+cu115 --extra-index-url https://download.pytorch.org/whl/cu115`
5. `cd` into the cloned repo
5. `pip install -e .`
6. `pip install -U openmim`
7. `mim install mmcv-full==1.6.2 -f https://download.openmmlab.com/mmcv/dist/{cuda_version}/{torch_version}/index.html`. Note that pre-built wheels (fast installs without needing to build) only exist for some versions of torch and CUDA. Check compatibilities here: https://mmcv.readthedocs.io/en/v1.6.2/get_started/installation.html
    1. e.g.: `mim install mmcv-full==1.6.2 -f https://download.openmmlab.com/mmcv/dist/cu115/torch1.11.0/index.html`


### Alternate Setup (Windows Users - Tested for Windows 10)

1. `conda create -n <environment-name> python=3.9`
2. `conda activate <environment-name>`
3. Install torch (tested for >=1.7.1 and <=1.11.0) and torchvision (tested for >=0.8.2 and <=0.12). May vary with your system. Please check at: https://pytorch.org/get-started/previous-versions/.
    1. e.g.: `pip install torch==1.11.0+cu113 torchvision==0.12.0+cu113 torchaudio==0.11.0 --extra-index-url https://download.pytorch.org/whl/cu113` 
4. `git clone https://github.com/NASA-IMPACT/hls-foundation-os.git <your-local-path>\hls-foundation-os`
5. `git clone https://github.com/open-mmlab/mmsegmentation.git <your-local-path>\mmsegmentation` 
6. `cd <your-local-path>\mmsegmentation` 
7. Checkout mmsegmentation version compatible with hls-foundation: `git checkout 186572a3ce64ac9b6b37e66d58c76515000c3280`
8. modify setup.py so it installs from the cloned mmsegmentation. Change line `mmsegmentation @ git+https://github.com/open-mmlab/mmsegmentation.git@186572a3ce64ac9b6b37e66d58c76515000c3280` to `mmsegmentation @ file:///<your-local-path>/mmsegmentation`
9. `cd <your-local-path>\hls-foundation-os`
10. `pip install -e .`
11. `pip install -U openmim`
12. `mim install mmcv-full==1.6.2 -f https://download.openmmlab.com/mmcv/dist/{cuda_version}/{torch_version}/index.html`. Note that pre-built wheels (fast installs without needing to build) only exist for some versions of torch and CUDA. Check compatibilities here: https://mmcv.readthedocs.io/en/v1.6.2/get_started/installation.html
    1. e.g.: `mim install mmcv-full==1.6.2 -f https://download.openmmlab.com/mmcv/dist/cu115/torch1.11.0/index.html`
13. `conda install -c conda-forge opencv`
14. `pip install datasets` 

### Acknowledgment
- [ibm-nasa-geospatial](https://huggingface.co/datasets/ibm-nasa-geospatial/multi-temporal-crop-classification)
- [hls-foundation-os](https://github.com/NASA-IMPACT/hls-foundation-os/)
