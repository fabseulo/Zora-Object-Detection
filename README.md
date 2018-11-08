# Zora-Object-Detection

Questa applicazione permette di effettuare l'object detection di un'immagine, sfruttando i modelli di TensorFlow caricati 
nel TensorFlow ModelServer.

## Prerequisiti
Per utilizzare l'applicazione è necessario scaricare i seguenti pacchetti:
```bash
pip install tensorflow
pip install grpcio
pip install numpy
pip install scipy
pip install object-detection
pip install hdfs
pip install tensorflow-serving-api
```
Per installare il ModelServer bisogna eseguire i seguenti passaggi:
```bash
echo "deb [arch=amd64] http://storage.googleapis.com/tensorflow-serving-apt stable tensorflow-model-server tensorflow-model-server-universal" | sudo tee /etc/apt/sources.list.d/tensorflow-serving.list && \
curl https://storage.googleapis.com/tensorflow-serving-apt/tensorflow-serving.release.pub.gpg | sudo apt-key add -
apt-get update && apt-get install tensorflow-model-server
```
