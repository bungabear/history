# GDG TensorFlow 19.04.06

[GDG Incheon](https://www.notion.so/GDG-Incheon-Songdo-616d056e03bb45beb59ee91910f7d466)

## 인공지능, 머신러닝, 딥러닝.

* [Google 머신러닝 코스](https://developers.google.com/machine-learning/crash-course/?hl=ko)

* 딥러닝 : 뉴런과 같은 구조를 이용하여 정보를 처리.
    * 여러개의 퍼셉트론과 퍼셉트론 층을 통해 구현하는 인공지능.
    * 퍼셉트론간의 Weight를 최적화하는 방식으로 학슴.

* 머신러닝의 종류
    * 지도학습  : 라벨이 있어야 한다.
    * 비지도학습 : 인풋만으로 학습
    * 강화학습 : input과 reword를 통해 학습

* 퍼셉트론 - 뉴런을 수학적으로 모델링.
    * input, weight, weighted sum, activation function, output으로 이루어짐
    * 단일 퍼셉트론으로는 XOR를 처리 못함.  
        -> 모든 논리게이트를 표현가능
    * 뉴런을 이용한 가산기 딥러닝 모델 : LSTM모델(https://ratsgo.github.io/natural%20language%20processing/2017/03/09/rnnlstm/)


* 선형회귀 : 입력에 비례하여 결과가 변하는 연산을 추론.
    * 선형함수가 활성화함수인 은닉층은 필요가 없다 -> 최적화 가능.

* Activation Function : ReLu가 많이 쓰인다. 왜?

* 비용함수 : Weight에 따른 오차(Cost)함수. 이 비용함수는 최저점이 있는 형태(최소 2차함수)이어야 한다. 그렇지 않으면 잘못된 학습 시도인듯.
    * Learning Late : Cost계산을 위한 Weight 변화 단위.
    * 경사도 하강법 (Gradient Decent)

* **오차 역전파** : 은닉층이 적으면 경사도 하강법으로 교정이 되지만, 은닉층이 많으면 너무 많은 미분 계산이 필요하다.(딥러닝의 1차 겨울)
    * 순방향으로 계산이 끝나면, Output에서 뒤로 오면서 편미분을 이용해 교청.

* **Vanishing Gradient 현상** : 은닉층이 많으면 출력층과 멀어질수록 학습이 잘 안됨.(딥러닝의 2차 겨울)
    * 시그노이드 활성화함수를 많이 썼는데, 거리가 멀수록 0에 수렵해버리기 때문.
    * ReLU 계열의 활성화 함수를 사용.

* 하이퍼파라메터 : 학습이 아닌 사람에의해 설정해야하는 변수들
    * 은닉층 레이어수
    * 은닉층 노드수 
    * 반복 합습 수
    * 가중치 초기값 
    * 입력데이터 정규화
    * 학습진도율
    * Cost Function
    * Min-batch 크기

* MNIST : 손 글씨 숫자 이미지 데이터. 28x28의 4만개의 트레이닝 이미지, 1만개의 테스트 이미지.
    * 0~9로 이미지 분류(output)
    * [테스트 사이트](https://colab.research.google.com/notebooks/welcome.ipynb)





# 알파고1 논문 리뷰

[몬테카를로 트리 서치](https://ko.wikipedia.org/wiki/%EB%AA%AC%ED%85%8C%EC%B9%B4%EB%A5%BC%EB%A1%9C_%ED%8A%B8%EB%A6%AC_%ED%83%90%EC%83%89)

* 너비를 줄임 : 무의미한 수를 배제
* 깊이를 줄임 : 게임 종료까지 가서 판단하지 않도록 함.

강화학습
* Policy network : 유의미한 수, 룰 계산 (너비를 줄임)
* Value network : 판세를 계산 (깊이를 줄임)


- SL(지도학습) policy network : 바둑서버의 3천만개 기보를 활용. 이를 통해 57% 정확도 달성

- Rollout policy : 작은 신경망으로 SL과 동일한 데이더 셋을 이용하지만 낮은 정확도, 빠른 계산용. 27% 정확도

- RL policy network : SL policy network의 weight 결과를 가져와 여러개의 network를 복제하여 서로간의 강화 학습. -> 80% 확률 (알파고1에서는 Value network를 만들때만 사용함.)

- Value Network : SL, RL과 같은 구조지만, output을 하나로 만들어 판세를 읽는데 사용. 예측률은 SL, RL과 비등하나 속도가 매우 빠름.

위의 4가지 네트워크를 통하여 몬테카를로 트리 탐색을 수행
 - 가지를 선택하여 좋은 수를 찾아 SL policy network를 통해 판단 하여, Value network로 Evaluation하면서 Rollout policy network로 가지를 탐색하여 평균 저장.

몬테카를로 트리 탐색은 학습된 전체 결과보다도 현재 연산 결과를 중시하는 경향이 있음.(많은 게임의 수에서 학습된것은 매우 일부라 보고, 현재 상태를 더 중시.)

#### DC/OS : yjyang@kbsys
#### jupyter notebook
