# Classificador de Imagens com CNN para o Dataset CIFAR-10

Este projeto implementa uma **Rede Neural Convolucional (CNN)** para classificar imagens do dataset **CIFAR-10**. O objetivo é construir e treinar um modelo capaz de reconhecer 10 categorias diferentes de objetos em imagens coloridas de baixa resolução.

---

## Dataset: CIFAR-10 🖼️

O [CIFAR-10](https://www.cs.toronto.edu/~kriz/cifar.html) é um dataset clássico utilizado para algoritmos de classificação de imagens. Ele é composto por:

* **60.000 imagens** coloridas de 32x32 pixels.
* **10 classes** de objetos, com 6.000 imagens por classe.

As 10 classes são: avião, automóvel, pássaro, gato, cervo, cachorro, sapo, cavalo, navio e caminhão.

---

## Tecnologias Utilizadas 🛠️

* **Python 3.x**
* **TensorFlow** e **Keras** para a construção e treinamento do modelo.
* **NumPy** para manipulação de arrays.

---

## Metodologia

O projeto segue as seguintes etapas para a construção e avaliação do classificador:

### 1. Pré-processamento dos Dados

Antes de alimentar a rede neural, os dados passaram pelas seguintes transformações:

* **Reshape:** As dimensões das imagens foram ajustadas para o formato que o TensorFlow espera: `(amostras, altura, largura, canais)`.
* **Normalização:** Os valores dos pixels, originalmente entre 0 e 255, foram normalizados para o intervalo entre **0 e 1**. Isso é feito dividindo todos os valores por 255, o que ajuda a acelerar a convergência durante o treinamento.
* **One-Hot Encoding:** Os rótulos (labels) das classes, que eram números inteiros de 0 a 9, foram convertidos para o formato categórico (vetores binários), que é o formato esperado pela função de perda `categorical_crossentropy`.

### 2. Arquitetura do Modelo

A Rede Neural Convolucional foi construída com a seguinte arquitetura:

| Camada | Tipo                 | Detalhes                                                 |
| :----- | :------------------- | :------------------------------------------------------- |
| 1      | `Conv2D`             | 32 filtros, kernel (3,3), ativação **ReLU** |
| 2      | `BatchNormalization` | Normaliza a saída da camada anterior                     |
| 3      | `MaxPooling2D`       | Janela de (2,2) para reduzir a dimensionalidade          |
| 4      | `Conv2D`             | 32 filtros, kernel (3,3), ativação **ReLU** |
| 5      | `BatchNormalization` | Normaliza a saída da camada anterior                     |
| 6      | `MaxPooling2D`       | Janela de (2,2)                                          |
| 7      | `Flatten`            | Transforma a matriz 2D em um vetor 1D                    |
| 8      | `Dense`              | Camada Densa com 128 neurônios, ativação **ReLU** |
| 9      | `Dropout`            | Regularização com taxa de **30%** para evitar overfitting |
| 10     | `Dense`              | Camada Densa com 128 neurônios, ativação **ReLU** |
| 11     | `Dropout`            | Regularização com taxa de **30%** |
| 12     | `Dense` (Saída)      | **10 neurônios** (1 para cada classe), ativação **Softmax** |

* **Otimizador:** `adam`
* **Função de Perda:** `categorical_crossentropy`

---


## Resultados 📊

O modelo foi treinado por 5 épocas, alcançando os seguintes resultados no conjunto de validação:

* **Acurácia de Validação Final:** **~69.88%**
* **Perda de Validação Final:** **~0.8929**
