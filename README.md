# kiwi-object-detection-UN

# Steps

1. Create CSV, images,frozen_model, output, TFRecords, train directories using the following command in the project root:

```shell
> bash initializeProject
```
2. Run `script/GetImages` notebook to get dataset images

3. Run `script/json_to_csv` notebook to convert the annotation files into a train and validation CSV files

4. Run `script/csv_to_tf` notebook to convert train and validation CSV into a tensorflow record

## Training locally

Change the following items in `faster_rcnn_resnet101_coco.config`

```json

model {
    ...
  faster_rcnn {
    num_classes: 16  //According with label_map.pbtxt
    ...
  }
}

...

train_config: {
  ...
  fine_tune_checkpoint: "model/model.ckpt"
  ...
}

...

train_input_reader: {
  tf_record_input_reader {
    input_path: "TFRecords/train.record"
  }
  label_map_path: "config/label_map.pbtxt"
}

...

eval_input_reader: {
  tf_record_input_reader {
    input_path: "validation.record"
  }
  label_map_path: "config/label_map.pbtxt"
  shuffle: false
  num_readers: 1
}

```

To run the training process
```
# in project root

export PYTHONPATH=$PYTHONPATH:`pwd`:`pwd`/slim

python object_detection/train.py --logtostderr --train_dir=train --pipeline_config_path=model/faster_rcnn_resnet101_coco.config
```

to freeze the model run

```
# in project root
python object_detection/export_inference_graph.py --input_type image_tensor --pipeline_config_path model/faster_rcnn_resnet101_coco.config  --trained_checkpoint_prefix train/model.ckpt-XXX --output_directory modelo_congelado

# Change XXX with the last step model in train directory
```

#Authors

- Juan Pablo Villegas Gomez. [@MrPaul91](https://github.com/MrPaul91)
- Sebastian Pino Sanchez. [@sebastianpinosanchez](https://github.com/sebastianpinosanchez)
- Santiago Restrepo Osorio. [@srestrepoo](https://github.com/srestrepoo)
- Giovani Hernán Cardona Sánchez



