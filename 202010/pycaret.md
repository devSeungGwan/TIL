# 개요

`pycaret`은 기존에 있던 Scikit-learn, XGBoost, LightGBM, spaCy 등 여러가지 머신러닝 라이브러리를 사용하기 용이하도록 ML High-Level API로 제작한 라이브러리입니다. 단 몇 줄만에 데이터 분석 및 머신러닝 모델 성능 비교까지 가능하고, Log 를 기본적으로 생성하여 이력을 남겨줍니다.

`pycaret`에서 제공하는 기능은 크게 5가지가 존재합니다.(링크를 누르면 예시 페이지로 넘어갑니다.)

* [Classification](https://github.com/pycaret/pycaret/blob/master/examples/PyCaret%202%20Classification.ipynb)
* [Regression](https://github.com/pycaret/pycaret/blob/master/examples/PyCaret%202%20Regression.ipynb)
* [Clustering](https://github.com/pycaret/pycaret/blob/master/examples/PyCaret%202%20Clustering.ipynb)
* [Anomaly Detection](https://github.com/pycaret/pycaret/blob/master/examples/PyCaret%202%20Anomaly%20Detection.ipynb)
* [Natural Language Processing](https://github.com/pycaret/pycaret/blob/master/examples/PyCaret%202%20NLP.ipynb)



# 기능

## 데이터 불러오기

`pycaret`은 학습을 위한 `Toy data`를 제공하고 있습니다. 제공하는 데이터의 정보는 `get_data('index')`를 통해 알 수 있습니다.

```python
from pycaret.datasets import get_data
index = get_data('index')
```

`Toy data` 중 `juice` 데이터를 가져옵니다. 데이터 포맷은 `pandas.DataFrame` 입니다.

데이터를 불러오면 데이터의 구조를 알 수 있도록 `.head(5)`가 기본적으로 실행됩니다.

```python
data = get_data('juice')
```

## setup

`pycaret`은 `setup` 객체를 사용하여 데이터에 대한 여러가지 머신러닝 기법들을 사용할 수 있습니다. 객체 선언 후 실행을 누른 후 Enter(취소 시 quit 입력)을 누릅니다. 실행 후 사용한 데이터에 대한 데이터 분석 결과를 제공합니다.

```python
from pycaret.classification import *
clf1 = setup(data, target='Purchase', session_id=123, log_experiment=True, experiment_name='exam_juice')
```

**실행 결과**

|      |                  Description |        Value |
| ---: | ---------------------------: | -----------: |
|    0 |                   session_id |          123 |
|    1 |                  Target Type |       Binary |
|    2 |                Label Encoded | CH: 0, MM: 1 |
|    3 |                Original Data |   (1070, 19) |
|    4 |               Missing Values |        False |
|    5 |             Numeric Features |           13 |
|    6 |         Categorical Features |            5 |
|    7 |             Ordinal Features |        False |
|    8 |    High Cardinality Features |        False |
|    9 |      High Cardinality Method |         None |
|   10 |                 Sampled Data |   (1070, 19) |
|   11 |        Transformed Train Set |    (748, 28) |
|   12 |         Transformed Test Set |    (322, 28) |
|   13 |              Numeric Imputer |         mean |
|   14 |          Categorical Imputer |     constant |
|   15 |                    Normalize |        False |
|   16 |             Normalize Method |         None |
|   17 |               Transformation |        False |
|   18 |        Transformation Method |         None |
|   19 |                          PCA |        False |
|   20 |                   PCA Method |         None |
|   21 |               PCA Components |         None |
|   22 |          Ignore Low Variance |        False |
|   23 |          Combine Rare Levels |        False |
|   24 |         Rare Level Threshold |         None |
|   25 |              Numeric Binning |        False |
|   26 |              Remove Outliers |        False |
|   27 |           Outliers Threshold |         None |
|   28 |     Remove Multicollinearity |        False |
|   29 |  Multicollinearity Threshold |         None |
|   30 |                   Clustering |        False |
|   31 |         Clustering Iteration |         None |
|   32 |          Polynomial Features |        False |
|   33 |            Polynomial Degree |         None |
|   34 |         Trignometry Features |        False |
|   35 |         Polynomial Threshold |         None |
|   36 |               Group Features |        False |
|   37 |            Feature Selection |        False |
|   38 | Features Selection Threshold |         None |
|   39 |          Feature Interaction |        False |
|   40 |                Feature Ratio |        False |
|   41 |        Interaction Threshold |         None |
|   42 |                Fix Imbalance |        False |
|   43 |         Fix Imbalance Method |        SMOTE |

## 모델 생성 및 비교

`pycaret`은 `setup` 이후 `compare_models()` 를 사용하여 머신러닝 모델들의 성능을 비교하거나, 모델을 선언하여 머신러닝해볼 수 있습니다. `model()` 을 사용하여 어떤 머신러닝 모델을 사용할 수 있는 지 확인할 수 있습니다.

### 모델 종류 확인

```python
model()
```

> 파라미터 이름, 머신러닝 기법 이름, 사이킷런 API, Turbo 사용 여부등을 알 수 있다.

### 모델 비교

```python
best_model = compare_model()
```

### 모델 생성(Linear Regression)

```python
lr = create_model('lr')
```

### 파라미터 튜닝

```python
tuned_lr = tune_model(lr)
```

### 앙상블 모델

```python
dt = create_model('dt')
bagged_dt = ensemble_model(dt) # 배깅
boosted_dt = ensemble_model(dt, method='Boosting') # 부스팅
```

### 블랜딩 앙상블

```python
blender = blend_models(estimator_list= [boosted_dt, bagged_dt, tuned_lr], method='soft')
```

### 스태킹 앙상블

```python
stacker = stack_models(estimator_list=[boosted_dt, bagged_dt, tuned_rf], meta_model=rf)
```

### 모델 차트 생성

머신러닝 모델에 대한 결과를 `plot_model()`을 사용한 차트를 생성할 수 있습니다. 해당 모델에 대한 다양한 차트를 보고 싶다면 `evaluate_model()`을 사용하여 여러가지 차트를 한번에 표시할 수 있습니다.

```python
plot_model(lr)
```

```python
plot_model(lr, plot='confusion_matrix')
```

```python
evaluate_model(lr)
```

### 모델 해석

classification 및 regression 모델에 한해서 훈련된 모델 객체를 받아서 해석할 수 있습니다. 해석은 SHAP(SHapley Additive exPlanations)를 기반으로 동작합니다.

```python
catboost = create_model('catboost', cross_validation=False)
```
```python
interpret_model(catboost)
```
![cat_int](https://images.velog.io/images/devseunggwan/post/775d4827-8d79-4aac-a499-0e8989b25ba7/image.png)

```python
interpret_model(catboost, plot='correlation')
```
![cat_dot](https://images.velog.io/images/devseunggwan/post/30700d86-2dc1-4826-9f44-0ce7233ecfc6/image.png)




# 결론

pycaret 이라는 머신러닝 라이브러리에 대해 알아보았다. scikit-learn을 래핑한 라이브러리라 Keras처럼 사용하기 편리하다는 장점이 있었다. 하지만 Keras는 Tensorflow에 종속되어 있어 Tensorflow에 대한 이해가 필요하듯이, pycaret도 scikit-learn에 대한 이해없이 사용은 가능하지만, scikit-learn 이해 이후 사용한다면, 좀 더 유동적인 프로그래밍이 가능하다. 그리고 pandas-profiling 처럼 쉽게 사용하는 만큼, 머신러닝 기초 지식을 많이 공부하여 분석 결과에 대한 분석, 기법에 대한 이해 등이 필요하다.

# Reference

https://pycaret.org/

https://github.com/pycaret/pycaret/