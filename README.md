# Zora-Object-Detection

This application is a simulation of server-side object detection into the prototype with Zora robot, using models loaded in the TensorFlow ModelServer.

## Prerequisites
Before to use the application, you need to download the following packages:
```bash
pip install tensorflow
pip install grpcio
pip install numpy
pip install scipy
pip install object-detection
pip install hdfs
pip install tensorflow-serving-api
```
To install the TensorFlow ModelServer, you need to run the following commands:
```bash
echo "deb [arch=amd64] http://storage.googleapis.com/tensorflow-serving-apt stable tensorflow-model-server tensorflow-model-server-universal" | sudo tee /etc/apt/sources.list.d/tensorflow-serving.list && \
curl https://storage.googleapis.com/tensorflow-serving-apt/tensorflow-serving.release.pub.gpg | sudo apt-key add -

sudo apt-get update
sudo apt-get install tensorflow-model-server
```

## Usage

First of all, you need to start the Model Server with the following command:
```bash
tensorflow_model_server --port=9000 --model_config_file='PATH_TO_BE_CONFIGURED/model_server.config'
```
Change PATH_TO_BE_CONFIGURED with the absolute path in your PC and change also the paths of models to load in the server, into the file **model_server.config**.

Then start the object detection of a choosen image (for example harry_meghan.jpg into Images_test directory) with the command:
```bash
python test.py --image_path=Images_test/harry_meghan.jpg
```
This script saves the predicted images with bounding boxes into Images_bbx directory and returns in output the results that into the prototype are passed to Zora robot: una stringa da far pronunciare al robot con le labels degli oggetti trovati (nel caso di maggior certezza), un vettore con le labels dei possibili oggetti (nel caso di incertezza) e il vettore nullo nel caso non vengano rilevati oggetti.

Se Hadoop è in esecuzione nel computer, l'applicazione salva un file di log e le immagini direttamente in HDFS.
