# dl_26_3
# Defect Detection
Детекция дефектов на поверхностях

## Getting started

Requirements

* Python >= 3.7
* GPU >= 16GB
* CUDA >= 11.3

1) Запуск обучения (модель U-Net):

````
$ python train_unet.py
````

2) Инференс (модель U-Net):

````
$ python inference_unet.py
````

## Dataset
Для обучения использовался набор данных Cracks on the Surface of the Construction (CrackForest Dataset), 
представленный по [ссылке](https://github.com/Charmve/Surface-Defect-Detection#9cracks-on-the-surface-of-the-construction).
Набор данных представляет собой аннотированную базу данных изображений трещин на поверхностях, которая может быть 
использована как представление общего состояние поверхности.

В наборе 11299 цветных изображений поверхностей с трещинами (файлы изображений извлечены на уровне пикселей).

## Model
Для решения задачи детекции дефектов на поверхности дорожных покрытий была выбрана сверточная нейронная сеть для 
сегментации изображений – U-Net. U-Net считается одной из стандартных архитектур CNN для задач сегментации изображений, 
когда нужно не только определить класс изображения целиком, но и сегментировать его области по классу, т. е. создать 
маску, которая будет разделять изображение на несколько классов. Архитектура состоит из стягивающего пути для захвата 
контекста и симметричного расширяющегося пути, который позволяет осуществить точную локализацию.

<p align="center"><img src="./imgs/u-net-architecture.png" alt="detection" width="50%"></p>

Обе обученные нами модели U-Net используют как основу предобученные resnet и vgg энкодеры. Обученные модели можно 
скачать по [ссылке](https://drive.google.com/drive/folders/16R0bpyHB9yJcPEL2J5yhRG7CfcIYxN1m?usp=sharing).

График потерь U-Net resnet и U-Net vgg:

<p align="center"><img src="./imgs/resnet_loss.png" alt="detection" width="30%"></p>

<p align="center"><img src="./imgs/vgg16_loss.png" alt="detection" width="30%"></p>

Параметры моделей таблице: 

|      Params      | U-Net resnet | U-Net vgg |
|:----------------:|:------------:|:---------:|
| Number of epochs |      10      |    10     |
|  Learning rate   |    0.001     |   0.001   |
|     Momentum     |     0.9      |    0.9    |
|    Batch Size    |      8       |     8     |
|   Weight_decay   |     1e-4     |   1e-4    |
|  Learning time   |              |           |

Результаты валидации на тестовой выборке представлены в таблице:

|  Metrix   | U-Net resnet | U-Net vgg |
|:---------:|:------------:|:---------:|
|   Loss    |     0.06     |   0.057   |

## Results
Примеры результаов работы модели представлены ниже. 
* U-Net resnet
Predicted mask:
<p align="left"><img src="./imgs/resnet_crack_in_large_context_03.jpg" alt="detection" width="30%"></p>
Визуализация:
<p align="left"><img src="./imgs/res_crack_in_large_context_03.jpg" alt="detection" width="50%"></p>

* U-Net vgg
Predicted mask:
<p align="left"><img src="./imgs/vgg_crack_in_large_context_03.jpg" alt="detection" width="30%"></p>
Визуализация:
<p align="left"><img src="./imgs/vgg16_crack_in_large_context_03.jpg" alt="detection" width="50%"></p>