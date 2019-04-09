# kiwi-object-detection-UN

# Steps

1. Create CSV, images,frozen_model, output, TFRecords, train directories using the following command in the project root:

```shell
> bash initializeProject
```
2. Run `script/GetImages` notebook to get dataset images

3. Run `script/json_to_csv` notebook to convert the annotation files into a train and validation CSV files

4. Run `script/csv_to_tf` notebook to convert train and validation CSV into a tensorflow record

#Authors

- Juan Pablo Villegas Gomez. [@MrPaul91](https://github.com/MrPaul91)
- Sebastian Pino Sanchez. [@sebastianpinosanchez](https://github.com/sebastianpinosanchez)



