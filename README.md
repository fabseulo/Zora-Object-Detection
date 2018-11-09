# Zora-Object-Detection

Questa applicazione è una simulazione della parte server dell'object detection di un'immagine con il robot Zora, sfruttando i modelli di TensorFlow caricati nel TensorFlow ModelServer.

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
Per installare il ModelServer bisogna eseguire i seguenti comandi:
```bash
echo "deb [arch=amd64] http://storage.googleapis.com/tensorflow-serving-apt stable tensorflow-model-server tensorflow-model-server-universal" | sudo tee /etc/apt/sources.list.d/tensorflow-serving.list && \
curl https://storage.googleapis.com/tensorflow-serving-apt/tensorflow-serving.release.pub.gpg | sudo apt-key add -

sudo apt-get update && apt-get install tensorflow-model-server
```

## Utilizzo

Avviare innanzitutto il ModelServer con il seguente comando:
```bash
tensorflow_model_server --port=9000 --model_config_file='PATH_TO_BE_CONFIGURED/model_server.config'
```
Sostituire PATH_TO_BE_CONFIGURED con il path nel proprio computer. Occorre, inoltre, modificare anche i path dei modelli all'interno del file **model_server.config**.

Avviare quindi l'object detection di un'immagine a scelta (ad esempio harry_meghan.jpg nella directory Images_test) con il comando:
```bash
python test.py --image_path=Images_test/harry_meghan.jpg
```
Lo script salva le immagini con i bounding box nella directory Images_bbx e restituisce i risultati da passare al robot Zora: una stringa da far pronunciare al robot con le labels degli oggetti trovati, nel caso di maggior certezza; un vettore con le labels dei possibili oggetti nel caso di incertezza e il vettore nullo nel caso non vengano rilevati oggetti.

Se Hadoop è in esecuzione nel computer, l'applicazione salva un file di log e le immagini direttamente in HDFS.
