# AlphaPose_Docker

## Guide

Here is a dockerfile help to set up a virtual enviornment for [AlphaPose](https://github.com/MVIG-SJTU/AlphaPose). Before set up, please check that the [docker](https://docs.docker.com/engine/install/ubuntu/) and [nvidia container toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html) are installed properly.

## Step
---
1. Install the dockerfile.
```
git clone https://github.com/nianjingfeng/AlphaPose_Docker.git
```
2. Build the docker image.
```
cd AlphaPose_Docker
docker build -t alphapose -f Dockerfile_alphapose .
```
3. Install AlphaPose code.
```
git clone https://github.com/MVIG-SJTU/AlphaPose.git
```
4. Install pretrain model and weight.
```
mkdir ./AlphaPose/detector/yolo/data
wget --load-cookies /tmp/cookies.txt "https://docs.google.com/uc?export=download&confirm=$(wget --quiet --save-cookies /tmp/cookies.txt --keep-session-cookies --no-check-certificate 'https://docs.google.com/uc?export=download&id=1D47msNOOiJKvPOXlnpyzdKA3k6E97NTC' -O- | sed -rn 's/.*confirm=([0-9A-Za-z_]+).*/\1\n/p')&id=1D47msNOOiJKvPOXlnpyzdKA3k6E97NTC" -O ./AlphaPose/detector/yolo/data/yolov3-spp.weights && rm -rf /tmp/cookies.txt
wget --load-cookies /tmp/cookies.txt "https://docs.google.com/uc?export=download&confirm=$(wget --quiet --save-cookies /tmp/cookies.txt --keep-session-cookies --no-check-certificate 'https://docs.google.com/uc?export=download&id=1kQhnMRURFiy7NsdS8EFL-8vtqEXOgECn' -O- | sed -rn 's/.*confirm=([0-9A-Za-z_]+).*/\1\n/p')&id=1kQhnMRURFiy7NsdS8EFL-8vtqEXOgECn" -O ./AlphaPose/pretrained_models/fast_res50_256x192.pth && rm -rf /tmp/cookies.txt
```
5. Build the docker container.
```
 docker run -it --gpus all -v ./AlphaPose:/~/home/AlphaPose alphapose /bin/bash
```
6. Run official build up file.
```
cd AlphaPose
python setup.py build develop
```
7. Demo using FastPose model.
```
mv scripts/demo_inference.py .
python demo_inference.py --cfg configs/coco/resnet/256x192_res50_lr1e-3_1x.yaml --checkpoint pretrained_models/fast_res50_256x192.pth --indir examples/demo/
```
8. Inference with other model.
- Please check the official document to download other models in [Model_ZOO](https://github.com/MVIG-SJTU/AlphaPose/blob/master/docs/MODEL_ZOO.md).
## Citation
---
[AlphaPose](https://github.com/MVIG-SJTU/AlphaPose)