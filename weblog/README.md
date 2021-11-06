## 정보보호와시스템보안 weblog Project

## 팀원
- 20191608 서형빈
- 20191600 박찬혁
- 20182249 최용렬

## EDA
- Http Method로서 GET, POST, PUT이 등장하는 것을 확인했습니다. 
- localhost의 포트번호는 8080, 9090만 등장하는 것을 확인했습니다. 
- anomal data 중에서 localhost:9090이 PUT method를 사용한 로그가 남은것을 확인했습니다. localhost:9090이 공격자이거나, PUT을 받는 기능이 서버에 없기 때문에 비정상적인 접근으로 처리되는 것으로 판단하여, localhost:9090이 PUT method를 가진 데이터를 보내는 경우 무조건 anomal으로 처리를 하였습니다. 처리 결과 SVM기준 accuracy가 약 0.5% 상승하였고, 정탐을 6개 더 잡을 수 있었습니다. 
- URL과 body를 제외하면 나머지 데이터들은 모두 동일 및 비슷한 데이터이거나, 해시값이기 때문에 그것이 악성인지 아닌지 판단하는데 큰 도움이 되지 않을 것이라 판단하여 피쳐에서 제외하였습니다. 

## Feature Engineering
- WebLog Header에서 http 버전은 고려하지 않았고, URI를 /를 기준으로 split하여 2-gram을 적용하였습니다. 또한, Http Method를 피쳐로 추가하였습니다. 
- http body는 &를 기준으로 key=value format입니다. 따라서 &, =으로 split하여 key, value를 피쳐로 사용했습니다. 

## Model Train & Test

#### LinearSVC(SVM)
- Accuracy: 0.9964791615491689
- Precision: 0.9979959919839679
- Recall: 0.9934171154997008
- F1-Score: 0.9957012896131161

#### RandomForest
- Accuracy: 0.9705232129697863
- Precision: 0.9412099374170302
- Recall: 0.9900259325753042
- F1-Score: 0.9650009721952169

#### XGBoost
- Accuracy: 0.9667567346270368
- Precision: 0.9398510597670422
- Recall: 0.9818471972870536
- F1-Score: 0.960390243902439

#### lightGBM
- Accuracy: 0.9700319331859494
- Precision: 0.9431623116536334
- Recall: 0.9864352683024137
- F1-Score: 0.9643135725429017
