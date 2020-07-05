# Colab-DeepDeblur

## Simply download `Colab-DeepDeblur.ipynb` and open it inside your Google Drive or click [here](https://colab.research.google.com/github/styler00dollar/Colab-DeepDeblur/blob/master/Colab-DeepDeblur.ipynb) and copy the file with "File > Save a copy to Drive..." into your Google Drive. 

This is a pytorch implementation of our research. Please refer to our CVPR 2017 paper for details:

Deep Multi-scale Convolutional Neural Network for Dynamic Scene Deblurring
[[paper](http://openaccess.thecvf.com/content_cvpr_2017/papers/Nah_Deep_Multi-Scale_Convolutional_CVPR_2017_paper.pdf)]
[[supplementary](http://openaccess.thecvf.com/content_cvpr_2017/supplemental/Nah_Deep_Multi-Scale_Convolutional_2017_CVPR_supplemental.zip)]
[[slide](https://drive.google.com/file/d/1sj7l2tGgJR-8wTyauvnSDGpiokjOzX_C/view?usp=sharing)]

If you find our work useful in your research or publication, please cite our work:
```
@InProceedings{Nah_2017_CVPR,
  author = {Nah, Seungjun and Kim, Tae Hyun and Lee, Kyoung Mu},
  title = {Deep Multi-Scale Convolutional Neural Network for Dynamic Scene Deblurring},
  booktitle = {The IEEE Conference on Computer Vision and Pattern Recognition (CVPR)},
  month = {July},
  year = {2017}
}
```

Original Torch7 implementaion is available [here](https://github.com/SeungjunNah/DeepDeblur_release).

#### Important information

- If you can't open `Colab-DeepDeblur.ipynb` inside your Google Drive, try this [colab link](https://colab.research.google.com/github/styler00dollar/Colab-DeepDeblur/blob/master/Colab-DeepDeblur.ipynb) and save it to your Google Drive. The "open in Colab"-button can be missing in Google Drive, if that person never used Colab.
- Google Colab does assign a random GPU. It depends on luck.
- The Google Colab VM does have a maximum session length of 12 hours. Additionally there is a 30 minute timeout if you leave colab. The VM will be deleted after these timeouts.

## Results

* Single-precision training results

Dataset | GOPRO_Large | REDS
:--:|:--:|:--:
PSNR | 30.40 | 32.89
SSIM | 0.9018 | 0.9207
Download | [link](https://drive.google.com/file/d/1-wGC6s2D2ba-PSV60AeHf48HtYd9JkQ4/view?usp=sharing) | [link](https://drive.google.com/file/d/1aSPgVsNcPNqeGPn0Y2uGmgIwaIn5Njkv/view?usp=sharing)

* Mixed-precision training results

Dataset | GOPRO_Large | REDS
:--:|:--:|:--:
PSNR| 30.42 | 32.95
SSIM| 0.9021 | 0.9209
Download | [link](https://drive.google.com/file/d/1TgiiiB-4lwWIIy8c-oSSkIy5g4GvDBKB/view?usp=sharing) | [link](https://drive.google.com/file/d/10hH5vtfGUUpy8jLvIBRCBqRoEhWRO1va/view?usp=sharing)

Mixed-precision training uses less memory and is faster, especially on NVIDIA Turing-generation GPUs.
Loss scaling technique is adopted to cope with the narrow representation range of fp16.
This could improve/degrade accuracy.

* Inference speed on RTX 2080 Ti (resolution: 1280x720)

Inference in half precision has negligible effect on accuracy while it requires less memory and computation time.
type | FP32 | FP16
:--:|:--:|:--:
fps | 1.06 | 3.03
time (s) | 0.943 | 0.330

## Models

To use the trained models, download files, unzip, and put them under DeepDeblur-PyTorch/experiment
* [GOPRO_L1](https://drive.google.com/file/d/1AfZhyUXEA8_UdZco9EdtpWjTBAb8BbWv/view?usp=sharing)
* [REDS_L1](https://drive.google.com/file/d/1UwFNXnGBz2rCBxhvq2gKt9Uhj5FeEsa4/view?usp=sharing)
* [GOPRO_L1_amp](https://drive.google.com/file/d/1ZcP3l2ZXj-C6yrDge5d3UxcaAKRN725w/view?usp=sharing)
* [REDS_L1_amp](https://drive.google.com/file/d/1do_HOjVFj2AYTX4BbwQ0enELRWtzhW6F/view?usp=sharing)

## Differences from the original code

The default options are different from the original paper.
* RGB range is [0, 255]
* L1 loss (without adversarial loss. Usage possible. See above examples)
* Batch size increased to 16.
* Distributed multi-gpu training is recommended.
* Mixed-precision training enabled. Accuracy not guaranteed.
* SSIM function changed from MATLAB to python
