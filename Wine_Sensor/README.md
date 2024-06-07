# 후각센서와 딥러닝을 활용하여 레드와인의 향 분류
<br>
## 1. 제안된 와인 향 식별 시스템 구성
본 실험에서 제안하는 와인 향 식별 시스템은 주요하게 입력 냄새에 대해 구성 화학성분을 감지하는 후각센서와 센서의 출력 데이터를 처리 및 와인 향을 분석 및 식별하는 LSTM 모델로 구성된다. 아래 그림은 제안된 화인 향 식별 시스템의 구성을 나타낸다.
![image](https://github.com/wonicom/Tabular_Model/assets/123945441/18dbb453-a92e-4935-861f-c5ccb3ddbfd5)<br>
후각센서로 사용된 Grove-Gas Sensor V2는 일산화탄소(CO), 이산화질소(NO2), 에틸알코올(C2H5CH), 휘발성 유기 화합물(VOC)의 가스를 감지할 수 있는 4개의 측정 장치로 구성되어 있다.<br>
 반복 신경망(Recurrent Neural Networks, RNN)의 일종인 LSTM은 순차적으로 입력되는 시계열 데이터를 현재 상태 정보와 함께 망각 게이트에서 저장된 과거 상태에 대해 집계 작업을 수행하여 미래 상태 정보를 계산한다. 또한, LSTM은 시간 경과에 따라 발생하는 후각센서의 느린 감도 변화로 발생하는 드리프트(Drift)현상을 시계열 데이터 처리로 보완할 수 있다.<br>
<br>
## 2. 실험 설계 및 결과 분석
제안된 시스템에 대한 성능 검증 실험을 위한 실험 설계 및 방법은 다음과 같다.
1. 와인향에 대해 훈련 및 식별을 위한 데이터 셋으로 Le Nez du Vin 레드 와인을 고려하였다. 해당 데이터 셋은 기본적으로 총 12가지 아로마 키트를 포함하고 있으며, 본 연구에서는 효율적인 실험 진행 및 성능 평가를 위해 12가지 아로마 키트 중 Blackcurrent, Smoky, Strawberry, Truffle, Violet 등 5가지 향을 선정하였다.<br>
2.  정확한 데이터 셋 측정 및 수집을 위해 실험 전 실험 공간을 환기하였고, 후각 센서와 아로마 키트를 포집 장치로 감싸 향의 공기중으로의 분산을 방지하였다.<br>
3. 딥러닝 처리를 위한 각 레드 와인 향에 대한 후각센서 출력 데이터 셋은 크게 훈련을 위한 Train-set, 유효 성능 평가를 한 Validation-set, 본격적인 성능을 측정하기 위한 Test-set으로 구분된다. 이때, 각각의 데이터 셋 길이는 순차적으로 7000 time-step, 1500 time-step, 1500 time-step이며, 1 time-step은 2초로 설정되었다. 또한, 딥러닝 입력 데이터 셋에 ’0’ 등의 결측치가 있는 경우, Preprocessing 과정을 통해 제거하였다. 그림 2는 Blackcurrent, Smoky, Strawberry, Truffle, Violet 등 5가지 향에 대한 후각센서 출력 데이터 셋을 나타낸다.<br>
![image](https://github.com/wonicom/Tabular_Model/assets/123945441/e6a537ae-c0ab-40b9-8f65-bb041c3bb014)
![image](https://github.com/wonicom/Tabular_Model/assets/123945441/98842000-b22e-4488-9a11-44e8a355c8a5)
![image](https://github.com/wonicom/Tabular_Model/assets/123945441/20d02c47-ecd6-400c-926d-503b7d8b5da5)
![image](https://github.com/wonicom/Tabular_Model/assets/123945441/59f1e013-2f8b-483a-b6b5-16ee8d08a32d)
![image](https://github.com/wonicom/Tabular_Model/assets/123945441/9e4b69ed-819e-43ea-ac98-90632ca76b87)
### 4. 정확한 실험 데이터 확보를 위해 컴퓨터 시스템 환경에서 수행되었다. 특히, 측정된 값은 Parallex에서 만든 PLX-DAQ 프로그램을 이용하여 CSV 파일에서 바로 데이터를 기록할 수 있도록 하였다.
### 5. 제안된 시스템의 와인 향 식별 성능 비교를 위해 LSTM 대신에 기존의 SVM(Support Vector Machine), Random Forest, KNN(K-Nearest Neighbor), MLP(Multi-Layer Perceptron), RNN 등 총 5개의 모델을 고려하였다. 이때, 각 시스템의 와인 향 식별 성능은 5가지 아로마 키트에 대한 평균 정확도 측정을 통해 평가되었다. 
<br>
제안된 시스템을 포함한 총 6가지의 와인 향 식별 시스템에 대한 평균 정확도 성능 분석 결과는 표 1과 같다. 표 1로부터, 와인 향 식별 정확도는 제안된 LSTM 기반 시스템이 약 97.6%로 RNN(약 95.7%), SVM(약 94.6%), Random Forest(약 92.8%), MLP(약 92.5%), KNN(57.3%) 기반의 시스템 보다 높음을 확인하였다.
![image](https://github.com/wonicom/Tabular_Model/assets/123945441/56355c37-d2bb-42ab-9b43-c49e07f56ac5)
<br>
## 3. 결론
본 실은 와인 향 식별의 정확도를 높이기 위해, 후각센서와 LSTM으로 구성된 진보된 전자코 시스템을 제안하였다. 특히, 제안된 시스템은 후각센서 Grove-Gas Sensor V2를 사용하여 와인 향 속의 복합적인 화학성분을 감지하도록 하였으며. LSTM을 사용하여 후각센서의 드리프트 문제를 보완하고 출력 데이터 셋을 심층적으로 분석하도록 하였다. 나아가, Blackcurrent, Smoky, Strawberry, Truffle, Violet 등 5가지 아로마 키트를 활용한 실험 결과를 통해 제안된 시스템의 우수한 와인 향 식별 성능을 확인하였다.
