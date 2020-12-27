# Transfer Learning

규모가 매우 큰 딥러닝 모델을 학습시킬 때 처음부터 새로 학습시키는 경우에 학습 속도가 느린 문제가 발생한다. 이러한 경우 기존에 학습된 비슷한 모델이 있을 때, 이 모델의 `하위층(Lower Layer)`을 가져와 재사용하는 것이 학습 속도를 빠르게 할 수 있을 뿐만 안니라 학습에 필요한 학습 데이터도 적게 사용하여 성능을 높힐 수 있다.

데이터 부족, 하드웨어 자원 부족, 오버슈팅 등 여러가지 기술 장벽들을 보완할 수 있다.



## Case

*New dataset is small and similar to original dataset*.

* 데이터가 작기 때문에 ConvNet을 미세조정하면 과적합 문제가 발생할 수 있다. 

* 데이터가 원본 데이터와 유사하기 때문에 ConvNet의 상위층(Upper Layer)도 학습하려는 데이터 셋과 연관이 있다.

*New dataset is large and similar to the original dataset*.

* 더 많은 데이터가 있기 때문에 전체 네트워크를 통해 Fine-Tuning하면 Over-Fitting 하지 않고 학습 속도를 높힐 수 있다.

*New dataset is small but very different from the original dataset*.

* 데이터가 작기 때문에 선형 분류기만 훈련하는 것이 가장 좋다. 데이터 셋이 매우 다르기 때문에 더 많은 데이터 셋 별 기능을 포함하는 네트워크 상단에서 학습하는 것은 좋지 않다. 

*New dataset is large and very different from the original dataset*.

* 데이터 셋이 크기 때문에 ConvNet 을 처음부터 훈련시킬 수 있다. 그러나 실제로도 사전 훈련된 모델의 가중치로 초기화하는 것이 여전히 유용하다. 

* 이 경우 전체 네트워크를 통해 미세조정하기에 충분한 데이터와 신뢰도를 갖게 된다.



## 제약 사항

학습하려는 데이터 셋이 학습된 데이터 셋과 유사성이 높으면 성능을 기대할 수 있지만, 데이터 셋이 완전히 다를 경우, 학습데이터를 처음부터 학습하는 것이 유리하다.

Merry의 경우, 사전에 준비된 블록데이터를 통해 `Pre-Train`된 모델을 생성한다. 이후, 실제 블록을 학습할 때 `Pre-Train` 된 데이터를 사용하여 신경망 파라미터를 초기화 한 후, 실제 블록을 학습한다. 이후 학습에는 기존에 학습된 블록의 모델을 가져와서 Fine-Tuning 하는 것이 성능 및 학습 속도에 영향을 줄 것으로 예상한다.



## 참조

https://cs231n.github.io/transfer-learning/