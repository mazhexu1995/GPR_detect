## Use improved yolo_v3 in GPR <br>




## Usage
1. clone YOLO_v3 repository
    ``` bash
    git clone https://github.com/mazhexu1995/GPR-yolo.git
    ```
2. prepare data<br>
    (1) Create a new folder named `data` in the directory where the `YOLO_V3` folder 
    is located, and then create a new folder named `VOC` in the `data/`.<br>
    
    The file structure is as follows:<br>
    |--YOLO_V3<br>
    |--data<br>
    |--|--VOC<br>
    |--|--|--2012_trainval<br>
    |--|--|--2007_trainval<br>
    |--|--|--2007_test<br>
    (2) convert data format<br>
    You should set `DATASET_PATH` in `config.py` to the path of the VOC dataset, for example:
    `DATASET_PATH = '/home/mzx/GPRyolo/data/VOC'`,and then<br>
    ```bash
    python voc_annotation.py
    ```
3. prepare initial weights<br>
    Download [YOLOv3-608.weights](https://pjreddie.com/media/files/yolov3.weights) firstly, 
    put the yolov3.weights into `yolov3_to_tf/`, and then 
    ```bash
    cd yolov3_to_tf
    python3 convert_weights.py --weights_file=yolov3.weights --dara_format=NHWC --ckpt_file=./saved_model/yolov3_608_coco_pretrained.ckpt
    cd ..
    python rename.py
    ``` 

4. Train<br>
    ``` bash
    python train.py
    ```
5. Test<br>
   
    ``` bash
    python test.py --gpu=0 --map_calc=True --weights_file=model_path.ckpt
    cd mAP
    python main.py -na -np
    ```

 
## Requirements
software
- Python2.7.12 <br>
- Numpy1.14.5<br>
- Tensorflow.1.8.0 <br>
- Opencv3.4.1 <br>

headware
- 12G 1080Ti