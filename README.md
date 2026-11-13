<h1 align="center">Real-Time Communication System Powered by AI for the Specially Abled</h1>

<p align="center"><b>Webcam sign-language letter recognition (A to I) with a Keras CNN and Flask.</b></p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/TensorFlow-FF6F00?logo=tensorflow&logoColor=white" alt="TensorFlow">
  <img src="https://img.shields.io/badge/Flask-000000?logo=flask&logoColor=white" alt="Flask">
  <img src="https://img.shields.io/badge/OpenCV-5C3EE8?logo=opencv&logoColor=white" alt="OpenCV">
</p>

A web app that reads sign-language letters from a webcam and shows the predicted letter live. A small CNN (Keras) classifies a hand sign into one of the letters **A to I**, and a Flask page streams the camera with the prediction drawn on top.

Letters J to Z are not supported. Several of them are gestures with movement, which a single-image classifier cannot capture.

## How it works

1. The webcam frame is resized to 640 x 480 and a fixed 200 x 200 box (the region of interest) is cut out.
2. The crop is scaled to 64 x 64 pixels and passed to the trained CNN.
3. The predicted letter is drawn on the video stream, which Flask serves as a live feed.

**Model** (`notebooks/train.ipynb`): one 3 x 3 convolution layer with 32 filters, max pooling, two dense layers (300 and 150 units) and a 9-way softmax. Images are 64 x 64 RGB with rescaling, zoom and horizontal-flip augmentation. Trained for 10 epochs with the Adam optimizer. The notebook notes an accuracy of 0.863.

## Run it

1. Download the **model** (`asl_model.h5`) and the **dataset**, then put the model into the `flask/` folder:
   - [Dataset](https://drive.google.com/drive/folders/1e8J-mUzHhPs394yFUMEDLaqbMBNemEKD)
   - [Model](https://drive.google.com/file/d/1NXq2WwmVUzNBdw3jI3yyYkK6GNv-y_AO/view?usp=drivesdk)
2. Install the requirements and start the app:

```sh
pip install -r requirements.txt
cd flask
python app.py
```

3. Open http://127.0.0.1:5000, click through to the live page and allow camera access. Hold your hand sign inside the box.

To retrain, point the two dataset paths in `notebooks/train.ipynb` at your copy of the dataset (they currently point to `C:/Project/datasetai/`). The notebook was written with an older TensorFlow 2 release: `fit_generator` is deprecated in current versions and `fit` replaces it.

## What is in the repo

```text
.
├── flask/                 web app: app.py, templates, static files
├── notebooks/             train.ipynb (training), test.ipynb (testing and webcam check)
├── docs/project.pdf       project documentation
└── requirements.txt
```

## Author

Dinesh Kumar Gudiputi, 2023
