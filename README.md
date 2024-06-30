# Faster-RCNN and YOLOv3 for Object Detection

## Used Framework
The project is built on top of the [mmdetection](https://mmdetection.readthedocs.io/zh_CN/latest/).

## How to train?
1. **Prepare the environment**: Users have to install the mmdetection framework and its dependencies. The installation guide can be found [here](https://mmdetection.readthedocs.io/zh_CN/latest/get_started.html). The project is **built-from-source** following the installation guide. After installation, `cd` into the `mmdetection` directory.
```bash
cd mmdetection
```
2. Prepare the dataset: Download the Pascal VOC dataset using the following command:
```bash
python tools/misc/download_dataset.py --dataset-name voc2007
```
  However, we need to transform the dataset into the COCO format. To do this, run the following command:
```bash
python voc_to_coco.py
```
  This script will create 3 annotation files in the VOCdevkit directory: `voc07_train.json`, `voc07_val.json`, and `voc07_test.json`. Then, we need to utilize the script `split.py` where you need to modify line4 and line6 in order to seperate images into training and validation and test sets. After that, you can create a new folder named coco inside `data` directory and move the `voc07_train.json`, `voc07_val.json`, and `voc07_test.json` files into the `coco` directory. Remember to rename the files to `instances_train2017.json`, `instances_val2017.json`, and `instances_test2017.json` respectively.
  After that, the `data/coco` directory should look like this:
  ```
  data/coco
  ├── annotations
  │   ├── instances_train2017.json
  │   ├── instances_val2017.json
  │   └── instances_test2017.json
  ├── test2017
  ├── train2017
  └── val2017
  ```

3. **Train the model**: To train the model, run the following command:
```bash
python tools/train.py configs/faster_rcnn/faster-rcnn_r50_fpn_1x_coco.py --work-dir ckpt/faster_rcnn
```


  or
```bash
python tools/train.py configs/yolov3/yolov3_d53_8xb8-ms-608-273e_coco.py --work-dir ckpt/yolov3
```
  The training process will start and the model will be saved in the `work_dirs` directory. One can visualize the loss using tensorboard.
4. **Test the model**: To test the model, run the following command:
```bash
python tools/test.py configs/faster_rcnn/faster-rcnn_r50_fpn_1x_coco.py ckpt/faster_rcnn/latest.pth --show-dir results/faster_rcnn
```
  
  or
```bash
python tools/test.py configs/yolov3/yolov3_d53_8xb8-ms-608-273e_coco.py ckpt/yolov3/latest.pth --show-dir results/yolov3
```
The testing process will start and the results will be saved in the `results` directory.

5. Inference: To perform inference on an image, run the following command:
```bash
python demo/image_demo.py path/to/your/image configs/faster_rcnn/faster-rcnn_r50_fpn_1x_coco.py ckpt/faster_rcnn/latest.pth --out-dir inference_results
```

## How to visualize the region proposals in the first stage of Faster-RCNN?

Run the command:
```bash
 python ./tools/test.py configs/rpn/rpn_r50_fpn_1x_coco.py path/to/your/ckpt --show-dir faster_rcnn_output2/rpn_proposal
```
## Pretrained model
Checkpoints are available at 链接: https://pan.baidu.com/s/1CSwTuAoM4eOzkBDr2FY2NA 提取码: tbjb 
--来自百度网盘超级会员v6的分享.
