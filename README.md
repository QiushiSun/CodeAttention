# CAT-probing: A Metric-based Approach to Interpret How Pre-trained Models for Programming Language Attend Code Structure

![License](https://img.shields.io/badge/License-MIT-blue) ![Build](https://img.shields.io/badge/Build-Passing-green) ![Last Commit](https://img.shields.io/github/last-commit/QiushiSun/CodeAttention)

## Updates

- 2022/12/10: Please check our [slides](https://drive.google.com/file/d/1Nb1QdwqFcmQuObRtSLZ-j3wNvp5qD89W/view?usp=share_link). 🐈
- 2022/10/12: Our code is available. 😋
- 2022/10/06: Release the paper of CAT-probing, check out our [paper](https://preview.aclanthology.org/emnlp-22-ingestion/2022.findings-emnlp.295/). 👏
- 2022/10/06: CAT-probing is accepted by **Findings of EMNLP 2022** 🎉

## Introduction

We proposed a metric-based probing method, namely, CAT-probing, to quantitatively evaluate how CodePTMs Attention scores relate to distances between AST nodes.

More details are provided in our EMNLP'22 paper and [our paper](https://preview.aclanthology.org/emnlp-22-ingestion/2022.findings-emnlp.295/).

## Environment & Preparing

```bash
conda create --name cat python=3.7
conda activate cat
pip install -r requirements.txt
git clone https://github.com/nchen909/CodeAttention
cd CodeAttention/evaluator/CodeBLEU/parser
bash build.sh
cd ../../../
cp evaluator/CodeBLEU/parser/my-languages.so build/
#make sure git-lfs installed like 'apt-get install git-lfs'
apt-get install git-lfs
bash get_models.sh
```

### Preparing data

The dataset we use comes from [CodeSearchNet](https://github.com/microsoft/CodeXGLUE/tree/main/Code-Text/code-to-text) .

```shell
mkdir data
cd data
pip install gdown
gdown https://drive.google.com/uc?export=download&id=1t8GncfPknpumOKbgUXux-EkuYnOZ6EfW
unzip data.zip
rm data.zip
```

### Preparing local path

Direct WORKDIR in run.sh and run_att.sh to your path.

## Using CAT-probing

### Finetune

```bash
export MODEL_NAME=
export TASK="summarize"
export SUB_TASK=
bash run.sh $MODEL_NAME $TASK $SUB_TASK
```

  `MODEL_NAME` can be any one of `["roberta", "codebert", "graphcodebert", "unixcoder"]`.

  `SUB_TASK` can be any one of `["go", "java", "javascript", "python"]`.

### Probing

```bash
# first modify WORKDIR in run_att.sh to yours 
export MODEL_NAME=
export TASK="summarize"
export SUB_TASK=
export LAYER_NUM=
bash run_att.sh $MODEL_NAME $TASK $SUB_TASK $LAYER_NUM
```

`MODEL_NAME` can be any one of `["roberta", "codebert", "graphcodebert", "unixcoder"]`.

`SUB_TASK` can be any one of `["go", "java", "javascript", "python"]`.

`LAYER_NUM` can be any one of `[0-11]` or `-1` (`11` refers to the last layer,  `-1` refers to all `[0-11]` layers).

## Visualization

Visualization results can be found in `att-vis-notebook` folder.

![Cat-probing](static/cat-probing-vis.jpg)

## Citation

Please consider citing us if you find this repository useful.👇

```bibtex
@inproceedings{chen2022cat,
    title     = "{CAT}-probing: A Metric-based Approach to Interpret How Pre-trained Models for Programming Language Attend Code Structure",
    author    = "Chen, Nuo  and Sun, Qiushi  and Zhu, Renyu  and
              Li, Xiang  and Lu, Xuesong  and Gao, Ming",
    booktitle = "Findings of the Association for Computational Linguistics: EMNLP 2022",
    month     = dec,
    year      = "2022",
    address   = "Abu Dhabi, United Arab Emirates",
    publisher = "Association for Computational Linguistics",
    url       = "https://aclanthology.org/2022.findings-emnlp.295",
    pages     = "4000--4008",
}
```

## Acknowledgement

This work has been supported by the National Natural Science Foundation of China under Grant No. U1911203, the National Natural Science Foundation of China under Grant No. 62277017, Alibaba Group through the Alibaba Innovation Research Program, and the National Natural Science Foundation of China under Grant No. 61877018, The Research Project of Shanghai Science and Technology Commission (20dz2260300) and The Fundamental Research Funds for the Central Universities.
