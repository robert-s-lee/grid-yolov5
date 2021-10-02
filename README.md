Grid.ai Session and Run examples of [Yolov5](https://github.com/ultralytics/yolov5)


- Configure Conda
```bash
conda create --yes --name yolov5 python=3.8
conda activate yolov5
```

- Install libraries
```bash
git clone https://github.com/ultralytics/yolov5
cd yolov5
pip install -r requirements.txt
```

- Download training data
Download into `../datasets` directory - 26GB

``` bash
python train.py --data coco.yaml --cfg yolov5s.yaml --weights '' --batch-size 64
python train.py --data coco.yaml --cfg yolov5m.yaml --weights '' --batch-size 40
python train.py --data coco.yaml --cfg yolov5l.yaml --weights '' --batch-size 24
python train.py --data coco.yaml --cfg yolov5x.yaml --weights '' --batch-size 16
```

- Grid.ai Datastore
```
grid datastore create --source ../datasets --name yolov5s
```

- Grid.ai Run
/gridai/project is where yolov5 is at
/gridai/datasets is where the Grid.ai datastore mount


```bash
libgl1-mesa-glx
```

```
grid run --datastore_name yolov5s --datastore_version 1 --datastore_mount_dir /gridai/datasets --dependency_file requirements.txt \
  train.py --data coco.yaml --cfg yolov5s.yaml --weights '' --batch-size 64

grid run --config grid_config.yaml train.py
```


Grid.ai Parallel Hyperparameter Optimization