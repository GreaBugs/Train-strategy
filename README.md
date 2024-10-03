# FastInst: A Simple Query-Based Model for Real-Time Instance Segmentation

[[`BibTeX`](#CitingFastInst)]

<p align="center"><img width="100%" src="figures/OverView_fig.png" /></p>

### Features

* The Multi-path Propagation of Queries (MPQ) strategy to address issues of feature degradation and cascading errors in the stage-wise decoding process.
* The Enhanced Mask Module (EMM) which improves mask quality and increases the diversity of masks used for attention computation.
* **State-of-the-art** higher accuracy under the same number of parameters and inference speed.
* Support major segmentation datasets: COCO, Cityscapes, ADE20K.

***

## Updates

* [2024/10] We have released the code and checkpoints for Training_strategy. Welcome to your attention!

## Installation

See [installation instructions](INSTALL.md).

## Getting Started

See [Results](#results).

See [Preparing Datasets for Training_strategy](datasets/README.md).

See [Getting Started](#getting-started-1).

***

# Results

<p><img width="50%" src="figures/compare_result1.png" /></p>
<p><img width="50%" src="figures/compare_result2.png" /></p>

### COCO Instance Segmentation

<table><tbody>
<!-- START TABLE -->
<!-- TABLE HEADER -->
<th valign="bottom">Name</th>
<th valign="bottom">Backbone</th>
<th valign="bottom">Epochs</th>
<th valign="bottom">Input</th>
<th valign="bottom">AP<sup>val</sup></th>
<th valign="bottom">Params</th>
<th valign="bottom">GFlops</th>
<th valign="bottom">download</th>

<tr>
<td align="left"><a href="configs/coco/instance-segmentation/fastinst_R50_ppm-fpn_x1_576.yaml">FastInst+EMM+MPQ</a></td>
<td align="center">R101</td>
<td align="center">50</td>
<td align="center">640</td>
<td align="center">40.0</td>
<td align="center">53.1M</td>
<td align="center">112.9</td>
<td align="center"><a href="https://github.com/junjiehe96/FastInst/releases/download/v0.1.0/fastinst_R50_ppm-fpn_x1_576_34.9.pth">model</a></td>
</tr>

<tr>
<td align="left"><a href="configs/coco/instance-segmentation/fastinst_R50_ppm-fpn_x1_576.yaml">FastInst+EMM+MPQ</a></td>
<td align="center">R50-d-DCN</td>
<td align="center">50</td>
<td align="center">640</td>
<td align="center">40.8</td>
<td align="center">34.7M</td>
<td align="center">68.0</td>
<td align="center"><a href="https://github.com/junjiehe96/FastInst/releases/download/v0.1.0/fastinst_R50_ppm-fpn_x1_576_34.9.pth">model</a></td>
</tr>

<tr>
<td align="left"><a href="configs/coco/instance-segmentation/fastinst_R50_ppm-fpn_x1_576.yaml">Mask2Former+EMM+MPQ</a></td>
<td align="center">R50</td>
<td align="center">50</td>
<td align="center">640</td>
<td align="center">44.3</td>
<td align="center">43.9M</td>
<td align="center">224.8</td>
<td align="center"><a href="https://github.com/junjiehe96/FastInst/releases/download/v0.1.0/fastinst_R50_ppm-fpn_x1_576_34.9.pth">model</a></td>
</tr>

<tr>
<td align="left"><a href="configs/coco/instance-segmentation/fastinst_R50_ppm-fpn_x1_576.yaml">Mask2Former+EMM+MPQ</a></td>
<td align="center">Swin-B</td>
<td align="center">50</td>
<td align="center">640</td>
<td align="center">48.7</td>
<td align="center">0.1G</td>
<td align="center">464.2</td>
<td align="center"><a href="https://github.com/junjiehe96/FastInst/releases/download/v0.1.0/fastinst_R50_ppm-fpn_x1_576_34.9.pth">model</a></td>
</tr>

</tbody></table>

# Getting Started

This document provides a brief intro of the usage of FastInst.

Please
see [Getting Started with Detectron2](https://github.com/facebookresearch/detectron2/blob/master/GETTING_STARTED.md) for
full usage.

#### Evaluate our pretrained models

* You can download our pretrained models and evaluate them with the following commands.
  ```sh
  python train_net.py --eval-only --num-gpus 4 --config-file config_path MODEL.WEIGHTS /path/to/checkpoint_file
  ```
  for example, to evaluate our released the fastest model, you can copy the config path from the table, download the
  pretrained checkpoint into `/path/to/checkpoint_file`, and run
  ```sh
  python train_net.py --eval-only --num-gpus 4 --config-file configs/coco/instance-segmentation/fastinst_R50_ppm-fpn_x1_576.yaml MODEL.WEIGHTS /path/to/checkpoint_file
  ```
  which can reproduce the model.

#### Train FastInst to reproduce results

* Use the above command without `eval-only` will train the model.
  ```sh
  python train_net.py --num-gpus 4 --config-file config_path
  ```
* For `R101` backbone, you need to
  download and specify the path of the pretrained backbones
  with `MODEL.WEIGHTS /path/to/pretrained_checkpoint`. The download link can be found in the above [table](#results).
  ```sh
  python train_net.py --num-gpus 4 --config-file config_path MODEL.WEIGHTS /path/to/pretrained_checkpoint
  ```
* For `R50-d-DCN` backbone, you need to download and convert the pretrained backbones, and specify the path.
  ```sh
  python tools/convert-timm-to-d2.py /path/to/resnet50d_ra2-464e36ba.pth /path/to/resnet50d_ra2-464e36ba.pkl
  python train_net.py --num-gpus 4 --config-file config_path MODEL.WEIGHTS /path/to/resnet50d_ra2-464e36ba.pkl
  ```

## LICNESE

FastInst is released under the [MIT Licence](LICENSE).

## <a name="CitingFastInst"></a>Citing FastInst

If you find FastInst is useful in your research or applications, please consider giving us a star &#127775; and citing
FastInst by the following BibTeX entry.

```BibTeX
@article{he2023fastinst,
  title={FastInst: A Simple Query-Based Model for Real-Time Instance Segmentation},
  author={He, Junjie and Li, Pengyu and Geng, Yifeng and Xie, Xuansong},
  journal={arXiv preprint arXiv:2303.08594},
  year={2023}
}
```

## Acknowledgement

Sincerely thanks to these excellent opensource projects

* [DETR](https://github.com/facebookresearch/detr)
* [Mask2Former](https://github.com/facebookresearch/Mask2Former)
