# Business_Analytics_ch5
# **[Ch.5] Semi-supervised Learning**
## VAT(Virtual Adversarial Training)

## 📂 Contents
-----------------------------
* Background
* Dataset
* Experiments
* Result
* Analysis

-----------------------------
### :pushpin: Background

## **Virtual Adversarial Training(VAT)**
<img src="./imgs/ba5/vat.jpg">
- 논문 : Virtual Adversarial Training: A Regularization Method for Supervised and Semi-Supervised Learning [paper](https://arxiv.org/abs/1704.03976)

> 기존 adversarial training에서는 조금의 변화로 모델의 예측을 크게 바꿀 수 있는 방향을 적대적 방향으로 
이용해 그 방향으로 만든 샘플들을 학습시켜 모델의 결정 경계를 부드럽게 만들어줌

- 입력 데이터에 간단한 변형이 아닌 adversarial한 변형 채택

- virtual adversarial loss : 각 input 데이터의 conditional label distribution의 robustness 표현

- adversarial: loss의 값을 최대한 해치는 방향으로 변형 (KL divergence 이용)

- virtual adversarial training : label 정보를 사용하지 않아 semi-supervised learning에 적용이 가능함
- regularization technique 이용 : overfitting 방지, unseen example들에 대해 잘 generaliza할 수 있게 함

- adversarial training과의 차이점 : label을 이용하여 adversarial perturbation 생성
- 입력 데이터는 x, 정답 라벨은 y, x*의 경우 입력 데이터 전체 의미
LDS(x^(n), \theta)

- **절차**
1. input data point x에서 시작
2. 작은 perturbation r을 이용하여 x를 변형시킴 + transform된 데이터 포인트는 T(x) = x + r
3. perturbation r (adversarial 방향에 있어야) perturb된 input은 perturb되지않은 input의 output과 달라야함 (2개의 output distribution 사이의 KL divergence는 최대화 되어야함,  r의 l2 normd은 작아야 함)
4. adversarial perturbation과 transform된 input을 찾은 이후, kl divergence가 최소화되는 방향으로 모델의 weight을 update 시켜주고, 모델을 각기 다른 perturbation에 대해 강건하게 만들어줌

- random perturbation training : vat에서 power iteration method를 쓰지 않는 열화판으로 무작위 방향으로 사용하는 방식

- vat는 가상의 적대적 방향에 해당하는 데이터에만 라벨을 할당하는 반면, RPT는 근방의 모든 데이터에게 동일한 라벨을 부여하므로 비효율적

#### [Tutorial]

### 📂 Dataset
----------------------------
* Street
View House Numbers (SVHN) [download](http://ufldl.stanford.edu/housenumbers/)
    - 10개의 class로 구성 (1개의 digit을 1개의 class로 설정)


* Cifar10 [download](https://www.cs.toronto.edu/~kriz/cifar.html)
    - 10개의 class로 구성
    - 32 x 42 크기의 이미지 60000장으로 구성


### 🖍️ Experiments
----------------------------
- SVHN 데이터셋 : epsilon 값을 바꿔가며 실험 진행
    - epsilon = 2.0, 2.5, 3.0으로 설정

- Cifar10 데이터셋 : label 수를 바꿔가며 실험 진행
    - labels = 1000, 2000, 4000으로 설정

### 📊 Result & Analysis
------------------------------
- SVHN 데이터셋
|**epsilon**|2.0|2.5|3.0|
|:--:|:--:|:--:|:--:|:--:|
|**accuracy**|0.8770|0.8635|0.8883|


- Cifar10 데이터셋
|**labels**|1000|2000|4000|
|:--:|:--:|:--:|:--:|
|**accuracy**|0.5148|0.5456|0.5745|

### 🖍️ Conclusion
------------------------------


### 📂 References
------------------------------
* https://github.com/pilsung-kang/Business-Analytics-IME654-
- 
