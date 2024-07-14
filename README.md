# Feature extract

## Models:

### UNI

- Trained on: 224x224 pixels @ 20x Mass-100K
- Weights: Found at [HuggingFace](https://huggingface.co/MahmoodLab/UNI)
- Paper: [Link to paper](https://www.nature.com/articles/s41591-024-02857-3)
- Repository: [GitHub Link](https://github.com/mahmoodlab/uni)


### CTransPath

- Trained on: 224x224 pixels @ ?
- Weights: [Download here](https://drive.google.com/file/d/1DoDx_70_TLj98gTf6YTXnu4tFhsFocDX/view)
- Paper: [Link to paper](https://www.sciencedirect.com/science/article/abs/pii/S1361841522002043)
- Repository: [GitHub link](https://github.com/Xiyue-Wang/TransPath)

### RetCCL

- Trained on: 256x256 pixels @ multiple scales
- Weights: [Download here](https://drive.google.com/drive/folders/1AhstAFVqtTqxeS9WlBpU41BV08LYFUnL)
- Paper: [Link to paper](https://www.sciencedirect.com/science/article/abs/pii/S1361841522002730)
- Repository: [GitHub link](https://github.com/Xiyue-Wang/RetCCL)

### Kimianet

- Trained on: 1000x1000 pixels @ 20x magnification
- Weights: [Download here](https://kimialab.uwaterloo.ca/kimia/index.php/sdm_downloads/kimianet-weights/)
- Paper: [Link to paper](https://arxiv.org/abs/2101.07903)
- Code Samples: [Download here](https://kimialab.uwaterloo.ca/kimia/index.php/sdm_downloads/kimianet-feature-extraction-code-samples/)

### SimCLRLung

- Trained on: 224x224 pixels @ 20x magnification
- Weights: [Download here](https://github.com/vkola-lab/tmi2022/blob/main/feature_extractor/model.pth)
- Paper: [Link to paper](https://ieeexplore.ieee.org/document/9779215)
- Repository: [GitHub link](https://github.com/vkola-lab/tmi2022)

### Resnet50

- Trained on: 224x224 Imagenet1k
- Weights: No need to download
- Paper: [Link to paper](https://arxiv.org/abs/1512.03385)
- Repository: [GitHub link](https://github.com/pytorch/vision/blob/main/torchvision/models/resnet.py)

### Segment Anything (SAM) EXPERIMENTAL

- Trained on: 1024x1024 @ Segmentation tasks
- 3 models: vit_b, vit_l, vit_h
- Outputs 256x64x64 feature maps, added average pooling so feature size is 256.
- Weights: Model checkpoint section at github repo
- Paper: [Link to paper](https://ai.facebook.com/research/publications/segment-anything/)
- Repository: [GitHub link](https://github.com/facebookresearch/segment-anything)

## Setup

To set up the environment, follow these steps:

1. Create your conda environment with dependencies:
   ``conda create --file environment.yml``
	
	you can change the environment name by editing the name tag in the environment.yml file or use the ``-n <environment_name>`` flag

2. Activate your conda environment
	``conda activate feature_ex``

## Usage

To start feature extraction, change the model paths in `model/model.py` to where you stored the weights, and then call the feature extraction script `feature_extraction.py` in the command line as follows:

```bash
python feature_extraction_new.py
	--slide_path /path/to/slides \ 
	--save_path /path/to/save \ 
	--file_extension .czi \  
	--models uni \ 
	--save_patch_images \ 
	--patch_size 256 \ 
	--invalid_ratio_thresh 0.5 \ 
	--edge_threshold 4 \ 
	--resolution_in_mpp 0 \ 
	--downscaling_factor 2 \ 
	-save_tile_preview \ 
	--preview_size 4096
```

To extract features from patch images instead of WSI use:

```bash
python feature_extraction_new.py
	--slide_path /path/to/slides \ 
	--save_path /path/to/save \ 
	--file_extension .tif \ 
	--models uni \ 
	--batch_size 512 \ 
	--patch_imgs
```

## Continue extraction

If for some reason the feature extraction was interrupted, you can specify a csv file with all files to extract features. A usefull command to get the not yet extracted features is
`` comm -23 <(ls folderA | sed 's/\.[^.]*$//') <(ls folderB | sed 's/\.[^.]*$//') > output.csv``
which returns all filenames that are in folderA but not folderB.
```