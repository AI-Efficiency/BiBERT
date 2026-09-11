# BiBERT: Accurate Fully Binarized BERT

**ICLR 2022**

Haotong Qin, Yifu Ding, Mingyuan Zhang, Qinghua Yan, Aishan Liu, Qingqing Dang, Ziwei Liu, Xianglong Liu

[Paper](https://openreview.net/forum?id=5xEgrl_5FAJ) | [arXiv](https://arxiv.org/abs/2203.06390) | [Citation](#citation)

**BiBERT enables 1-bit weights, word embeddings, and activations in BERT using information-preserving Bi-Attention and Direction-Matching Distillation (DMD).** It targets the accuracy loss of fully binarized language encoders and requires task data and a full-precision teacher for training.

## Published results

BERT-base on the GLUE development sets, **without data augmentation** (Table 2). W/E/A denotes weights/word embeddings/activations. The average follows the paper's aggregation of GLUE metrics; it is not a single-task accuracy. The FLOPs column uses the paper's bit-operation accounting.

| Method | W/E/A | Model size (MB) | FLOPs (G) | GLUE average |
| --- | --- | --- | --- | --- |
| Full precision | 32/32/32 | 418 | 22.5 | 83.9 |
| BinaryBERT | 1/1/4 | 16.5 | 1.5 | 79.9 |
| BinaryBERT | 1/1/1 | 16.5 | 0.4 | 41.0 |
| Fully binary baseline | 1/1/1 | 13.4 | 0.4 | 50.4 |
| BiBERT | 1/1/1 | 13.4 | 0.4 | 63.2 |

The reported **56.3× FLOPs reduction and 31.2× model-size reduction** are relative to full-precision BERT-base (Section 4.2). They are theoretical computation and parameter storage figures, not measured latency or peak runtime memory. Higher-bit BinaryBERT still has higher average accuracy in the 1/1/4 setting above.

### What this paper supports

- Bi-Attention addresses the information bottleneck caused by binarizing attention probabilities (Section 3.2).
- DMD transfers query/key/value similarity patterns to alleviate optimization-direction mismatch in distillation (Section 3.3).
- Combining Bi-Attention and DMD improves SST-2 from 77.6 to 88.7 without augmentation in the BERT-base ablation (Table 1).
- Under the fully binary comparison without augmentation, BiBERT raises the GLUE average from 50.4 to 63.2 over the straightforward baseline (Table 2).
- The method extends to the evaluated 6-layer and 4-layer TinyBERT architectures; data-augmented results are reported separately (Tables 2 and 3).

## Code and usage

Created by [Haotong Qin](https://htqin.github.io/), [Yifu Ding](https://yifu-ding.github.io/), [Mingyuan Zhang](https://scholar.google.com/citations?user=2QLD4fAAAAAJ&hl=en), Qinghua Yan, [Aishan Liu](https://liuaishan.github.io/), Qingqing Dang, [Ziwei Liu](https://liuziwei7.github.io/), and [Xianglong Liu](https://xlliu-beihang.github.io/) from Beihang University, Nanyang Technological University, and Baidu Inc. [[PaddlePaddle Version]](https://github.com/PaddlePaddle/PaddleSlim/tree/develop/demo/quant/BiBERT)

![loading-ag-172](./resources/overview.png)

## Dependencies

```shell
pip install -r requirements.txt
```

## Datasets

The paper reports GLUE experiments. This repository also retains SQuAD-related code from its upstream implementations; the GLUE results above do not establish a SQuAD result. Dataset resources:

- **GLUE**: https://github.com/nyu-mll/GLUE-baselines
- **SQuAD**: https://rajpurkar.github.io/SQuAD-explorer/

For data augmentation on GLUE, please follow the instruction in [TinyBERT](https://github.com/huawei-noah/Pretrained-Language-Model/tree/master/TinyBERT).

## Execution

Our experiments are based on the fine-tuned full-precision DynaBERT, which can be found [here](https://drive.google.com/file/d/1pYApaDcse5QIB6lZagWO0uElAavFazpA/view?usp=sharing). Complete running scripts and more detailed tips are provided in `./scripts`. Go through each script for more detail, and our corresponding well-trained BiBERT models are provided in [here](https://drive.google.com/drive/folders/1xEEIynvsYuqqG6wRlMhSySUusZWoR1FL?usp=sharing).

## Acknowledgement

The original code is borrowed from [BinaryBERT](https://github.com/huawei-noah/Pretrained-Language-Model/tree/master/BinaryBERT) and [DynaBERT](https://github.com/huawei-noah/Pretrained-Language-Model/tree/master/DynaBERT).

## Citation

Please cite the published paper below. Open paper versions are linked at the top of this README.

```bibtex
@inproceedings{Qin:iclr22,
  title = {{BiBERT}: Accurate Fully Binarized {BERT}},
  author = {Haotong Qin and Yifu Ding and Mingyuan Zhang and Qinghua Yan and Aishan Liu and Qingqing Dang and Ziwei Liu and Xianglong Liu},
  booktitle = {International Conference on Learning Representations},
  year = {2022},
  url = {https://openreview.net/forum?id=5xEgrl_5FAJ}
}
```
