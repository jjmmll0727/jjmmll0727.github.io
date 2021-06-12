---
title: "smile detection code review - train"
categories: "deep-learning"
excerpt: "reviewing train.py"
header:
  teaser: ../assets/images/fall.jpg
---
<style>
code {
  font-family: Consolas,"courier new";
  padding: 2px;
  font-size: 90%;
}
</style>

<div style = "font-size: 20px; line-height: 25px;">
<center>train.py</center><br><br>
</div>

```python
import argparse
import numpy             as np
import matplotlib.pyplot as plt
import sys

sys.path.insert(1, '../')

from keras.utils                  import np_utils
from dataset.datasetloader        import DatasetLoader
from sklearn.metrics              import classification_report
from sklearn.preprocessing        import LabelEncoder
from sklearn.model_selection      import train_test_split
from networks.convolutional.lenet import LeNet

def main():
    print("[INFO] loading dataset...")
    data, labels, args = loadDataset()

    print("[INFO] applying one-hot encoding to labels...")
    label_encoder, labels = oneHotEncoding(labels)

    print("[INFO] computing class weights to compensate data imbalance")
    class_weight = computeClassWeight(labels)

    print("[INFO] partitioning data into training and testing...")
    (X_train, X_test, y_train, y_test) = train_test_split(data, labels,
                                                          test_size=0.3,
                                                          stratify=labels,
                                                          random_state=13)

    print("[INFO] compiling model...")
    lenet_model = createModel()

    print("[INFO] training network...")
    model_history = trainModel(lenet_model, X_train, X_test,
                               y_train, y_test, class_weight)

    print("[INFO] evaluating network...")
    evaluateNetwork(lenet_model, model_history, label_encoder, X_test, y_test)

    print("[INFO] serializing network...")
    lenet_model.save(args["model"])

def getArguments():
    arg_parser = argparse.ArgumentParser()
    arg_parser.add_argument("-d", "--dataset", required=True,
                    help="path to input dataset of faces")
    arg_parser.add_argument("-m", "--model", default="lenet_smiles.hdf5",
                    help="path to save model")
    return vars(arg_parser.parse_args())

def loadDataset():
    args = getArguments()
    dataset_loader = DatasetLoader(args["dataset"])
    (data, labels) = dataset_loader.load(verbose=100)
    return data, labels, args

def oneHotEncoding(labels):
    label_encoder = LabelEncoder().fit(labels)
    labels = np_utils.to_categorical(label_encoder.transform(labels), 2)
    return label_encoder, labels

def computeClassWeight(labels):
    class_totals = labels.sum(axis=0)
    class_weight = class_totals.max() / class_totals
    return class_weight

def createModel():
    lenet_model = LeNet(width=28, height=28, depth=1, classes=2)
    lenet_model.build()
    lenet_model.compile(loss_function="binary_crossentropy",
                        optimizer="adam", metrics_list=["accuracy"])
    return lenet_model

def trainModel(model, data_train, data_test, label_train,
               label_test, class_weight):
    return model.trainNetwork(data=data_train, labels=label_train,
                             validation_data=(data_test, label_test),
                             class_weight=class_weight, batch_size=64,
                             epochs=15)

def evaluateNetwork(model, model_history, label_encoder, data, labels):
    predictions = model.predict(data, batch_size=64)
    print(classification_report(labels.argmax(axis=1),
                                predictions.argmax(axis=1),
                                target_names=label_encoder.classes_))
    plot(model_history)

def plot(history):
    plt.style.use("ggplot")
    plt.figure()
    plt.plot(np.arange(0, 15), history.history["loss"], label="train_loss")
    plt.plot(np.arange(0, 15), history.history["val_loss"], label="val_loss")
    plt.plot(np.arange(0, 15), history.history["accuracy"], label="acc")
    plt.plot(np.arange(0, 15), history.history["val_accuracy"],
             label="val_acc")
    plt.title("Loss and Accuracy")
    plt.xlabel("Epoch")
    plt.ylabel("Loss/Accuracy")
    plt.legend()
    plt.show()

if __name__ == '__main__':
    main()
```

<br>
<div>
   <p style = "text-align: left; font-size: 15px">
   여기서는 data들을 어떻게 전처리를 통해서 model의 input으로 들어가는지 파악하는 것이 중요하다.  
   </p>
</div>
<br>
<div style = "font-size: 23px; line-heignt:2em; font-family: fantasy;">
<strong>1. oneHotEncoding(labels) </strong><br>
</div>

```python
def oneHotEncoding(labels):
    label_encoder = LabelEncoder().fit(labels)
    labels = np_utils.to_categorical(label_encoder.transform(labels), 2)
    return label_encoder, labels
```

<div>
<p style = "font-size: 15px; text-align: left; line-heignt:3em;">
sklearn.preprocessing에서 LabelEncoder() 내장 함수를 가져오는데, LabelEncoder 객체를 생성하는 역할이다. 
객체를 생성하고 fit 함수와 transforms 함수를 통해 레이블 인코딩을 수행한다.<br>
1차원의 데이터가 형성되는데, 할당 되는 정수값에 의해 임의로 부여되는 가중치 혹은 중요도의 차이가 생길 수 있다.
그렇기 때문에, 1차원을 2차원으로 바꿔줘야 하는데 바꿔주는 함수가 <strong>np_utils package의 to_categorical</strong> 함수이다.
</p><br><p style = "font-size: 10px;"><a href = "https://2-chae.github.io/category/1.ai/30">출처</a></p><br>
</div>
<p style = "font-size: 20px; text-align:left">testing</p>

```python
from sklearn.preprocessing import LabelEncoder
from keras.utils import np_utils

list = ['smiling', 'smiling', 'non-smiling', 'smiling', 'smiling', 'smiling', 'non-smiling',
'non-smiling', 'smiling', 'non-smiling', 'non-smiling', 'non-smiling', 'smiling', 'non-smiling',
'smiling', 'smiling', 'smiling', 'smiling', 'smiling', 'smiling', 'smiling', 'smiling',
'smiling', 'smiling', 'smiling', 'smiling', 'smiling']

encoder = LabelEncoder().fit(list)
print(encoder.transform(list))

labels = np_utils.to_categorical(encoder.transform(list))
print(labels)

```

<br>
<div>
<center><img src = "\assets\images\to_categorical.png" border=0></center>
<br>
<p style = "font-size: 15px; text-align: left"><strong>1차원 데이터가 label_encoder / 2차원 데이터가 labels의 역할이다. </strong></p><br>
</div>

<div style = "font-size: 23px; line-heignt:2em; font-family: fantasy;">
<strong>2. computeClassWeight(labels) </strong><br>
</div>

```python
def computeClassWeight(labels):
    class_totals = labels.sum(axis=0)
    class_weight = class_totals.max() / class_totals
    return class_weight
```

<div>
<p style = "font-size: 15px; text-align: left; line-heignt:3em;">
<strong>클래스 불균형</strong><br>
데이터의 비중이 쏠리는 현상을 말한다. <br>
사전에 준비된 데이터의 label의 비중이 예를들어, smiling 80%, non-smiling 20% 일 경우, accuracy만 따진다면 불균형을 해소할 필요가 없지만, 그렇지 않다면 non-smiling에 더 많은 가중치를 두어 균형을 맞추는 작업이 필요하다. <br> 이를 클래스 불균형 해소라고 한다. 높은 성능을 내기 위해 반드시 필요한 작업이다. 
</p><br><p style = "font-size: 10px;"><a href = "https://3months.tistory.com/414">출처</a></p><br>
</div>
<p style = "font-size: 20px; text-align:left">testing</p>

```python
reshape = labels.sum(axis = 0)
print(reshape)

print(reshape.max()/reshape)
```

<div>
<center><img src = "\assets\images\weight_balancing.png" border=0 ></center>
<p style = "font-size: 15px; text-align: left"><strong> 2.857143 / 1. 값들이 smiling / non-smiling의 가중치라고 생각하면 된다.</strong></p><br>
</div>

<div style = "font-size: 23px; line-heignt:2em; font-family: fantasy;">
<strong>3. trainModel(model, data_train, data_test, label_train, label_test, class_weight) </strong><br>
</div>

```python
def trainModel(model, data_train, data_test, label_train,
               label_test, class_weight):
    return model.trainNetwork(data=data_train, labels=label_train,
                             validation_data=(data_test, label_test),
                             class_weight=class_weight, batch_size=64,
                             epochs=15)

(X_train, X_test, y_train, y_test) = train_test_split(data, labels,
                                                          test_size=0.3,
                                                          stratify=labels,
                                                          random_state=13)
```

<div>
<p style = "font-size: 15px; text-align: left; line-heignt:3em;">
<strong>모델 학습시키기</strong><br>
사전에 준비된 data들로만 학습을 시키면 overfitting(과적합)현상이 일어날 수 있다.<br>
새로운 데이터로 test를 하면 낮은 accuracy를 보일 수 있기 때문에, 사전에 준비된 data와 label들을 train data,label & validation data,label로 나눠서 training을 해야한다.<br>
train_test_split() 함수를 통해 사전에 준비된 data와 label들을 나눠준다.<br>
test_size는 사전 data들 중 validation 데이터로 전환할 비율을 말한다. 즉, 100개의 data들 중 30개를 validation data로 바꾼다.<br>
shuffle: default(True) train data와 validation data를 무작위로 훈련한다.<br>
만약, validation data를 학습하는 도중 error가 발생하면 exit 하고 다시 훈련한다. 
</p><br><br>
</div>
