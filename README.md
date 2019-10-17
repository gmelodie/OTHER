# OTHER
Yet another **O**p**T**ical c**H**aract**E**r **R**ecognizer


## Installation
It is strongly advised to use a [virtual environment](https://docs.python.org/3/library/venv.html) to install and run this project. Also, make sure you are running Python 3.6 or newer.

Install dependencies:
```
$ pip install -r requirements.txt
```

## Training the model

To retrain the pretrained model:

```
$ python3 retrain.py --image_dir <images dir>
```

Where `<images dir>` is the directory containing the training images separated by their classes. For example, suppose we want our network to choose between dogs and cats. Our directory tree would look like this:

```
images
├── cat
│   ├── cat10.jpg
│   ├── cat1.jpg
│   ├── cat2.jpg
│   ├── cat3.jpg
│   ├── cat4.jpg
│   ├── cat5.jpg
│   ├── cat6.jpg
│   ├── cat7.jpg
│   ├── cat8.jpg
│   └── cat9.jpg
└── dog
    ├── dog10.jpg
    ├── dog1.jpg
    ├── dog2.jpg
    ├── dog3.jpg
    ├── dog4.jpg
    ├── dog5.jpg
    ├── dog6.jpg
    ├── dog7.jpg
    ├── dog8.jpg
    └── dog9.jpg
```

And we would call the program like so:

```
$ python3 retrain.py --image_dir images
```

The trained model will be available in `/tmp/output_graph.pd`, and the labels in `/tmp/output_labels.txt`.


## Visualizing results

The script automatically saves the logs of the retraining in `/tmp/retrain_logs`, you can change this with the `--summaries_dir` flag. To view the summaries, use `tensorboard`:

```
$ tensorboard --logdir <summary dir>
```

## Predicting new images

Use the `label_image.py` script to load the trained model (`output_graph.pd`) and the labels (`output_labels.txt`) and predict new images:

```
python label_image.py --graph=<GRAPH> --labels=<LABELS> --input_layer=Placeholder --output_layer=final_result --input_height=224 --input_width=224 --image=<IMAGE>
```


## Other options

- `retrain.py`
    `--output_graph <OUT_GRAPH>`: Specify output path for graph file
    `--output_labels <OUT_LABELS>`: Specify output path for labels file
    `--sumaries_dir <SUM_DIR>`: Specify output path for summary files
    `--how_many_training_steps <TRAIN_STEPS>`: Specify the number of training steps to run
