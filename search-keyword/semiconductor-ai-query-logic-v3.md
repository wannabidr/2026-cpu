# V3 검색식 논리 설명서

이 문서는 `semiconductor-ai-total-combined-query.md`에 저장된 **V3 - A11 반도체 제조 데이터 AI 특허 검색식**이 어떤 특허를 찾으려는지 영역별로 설명한다.

## 한 줄 요약

V3 검색식은 단순히 “반도체 + AI” 특허를 찾는 식이 아니다.

목표는 **반도체/디스플레이/솔라 제조 공정에서 발생하는 장비 데이터, 공정 데이터, 검사/계측/수율 데이터를 AI/ML로 분석, 진단, 예측, 제어, 최적화하는 특허**를 찾는 것이다.

## 전체 논리 구조

```text
A. 반도체 제조 영역
AND
B. 제조/장비/검사 데이터 영역
AND
C. AI 분석/진단/예측/제어 영역
NOT
D. 의료, 차량, 일반 UI, 배터리 등 노이즈 영역
```

즉 검색 결과에 남으려면 기본적으로 아래 세 조건을 모두 만족해야 한다.

1. 반도체 제조 또는 그에 준하는 디스플레이/솔라 제조 문맥이 있어야 한다.
2. 장비 데이터, 공정 데이터, 웨이퍼/기판/패널 검사 결과 같은 제조 데이터 문맥이 있어야 한다.
3. AI, 머신러닝, 딥러닝, 가상계측, 이상탐지, 고장진단, 결함분류, 수율예측, 공정제어, 레시피최적화 같은 기능 문맥이 있어야 한다.

그리고 의료, 차량, 일반 디스플레이 UI, 배터리, 일반 소프트웨어 AI처럼 V2에서 대량으로 유입된 노이즈는 제외한다.

## A. 반도체 제조 영역

이 영역은 “해당 특허가 반도체 제조 쪽인가?”를 확인하는 관문이다.

### 포함하려는 기술

- 반도체 제조, 반도체 공정, 반도체 장비
- 웨이퍼 제조, 웨이퍼 처리, 웨이퍼 검사, 웨이퍼 계측
- 기판 처리, 기판 검사, 기판 계측
- 공정 챔버, 처리 챔버, 플라즈마 챔버, 식각 챔버, 증착 챔버
- 식각, 증착, 노광, 리소그래피, CMP, 세정, 열처리, 이온주입
- 오버레이 계측, CD-SEM, 마스크 검사, EUV 리소그래피

### 대표 키워드

```text
semiconductor manufacturing
semiconductor processing
semiconductor equipment
wafer processing
wafer inspection
wafer metrology
substrate processing
etching process
deposition process
lithography
overlay metrology
CD-SEM
mask inspection
EUV lithography
```

### 왜 이렇게 구성했는가

V2에서는 `semiconductor`, `display`, `substrate` 같은 단독어가 너무 넓게 작동했다. 그래서 V3에서는 단순 제품명보다 **제조/공정/장비/검사/계측 문맥**이 드러나는 표현을 중심으로 구성했다.

## 디스플레이/솔라 확장 영역

A11 문제 범위에는 반도체뿐 아니라 디스플레이, 태양전지, 솔라셀, 광전지도 포함될 수 있다. 다만 V2에서 일반 표시장치, 차량 디스플레이, HMD, UI 특허가 많이 들어왔기 때문에 V3에서는 디스플레이/솔라를 더 조심스럽게 잡는다.

### 포함하려는 기술

- 디스플레이 제조, 디스플레이 공정
- 패널 제조, 패널 검사, 패널 계측
- OLED 제조, OLED 증착
- TFT array 공정
- 글라스 기판 처리, 글라스 기판 검사
- 태양전지 제조, 태양전지 공정, 태양전지 검사
- photovoltaic manufacturing, PV cell fabrication

### 핵심 논리

`display`라는 단어만으로는 통과시키지 않는다.

아래처럼 제조/검사/계측 문맥이 붙은 경우를 우선한다.

```text
display manufacturing
display fabrication
display defect inspection
panel inspection
panel metrology
glass substrate processing
solar cell manufacturing
solar cell inspection
photovoltaic process
```

## B. 제조/장비/검사 데이터 영역

이 영역은 “AI가 분석할 데이터가 있는가?”를 확인하는 관문이다.

V3에서는 데이터를 세 종류로 본다.

## B-1. 장비 데이터

장비에서 직접 발생하는 센서값, 로그, 상태값, 트레이스 데이터를 말한다.

### 포함하려는 데이터

- 장비 데이터, 툴 데이터, 챔버 데이터
- 장비 로그, 공정 로그, 이벤트 로그
- 센서 신호, 공정 신호, in-situ signal
- time-series data, trace data
- 챔버 압력, 챔버 온도, 웨이퍼 온도
- RF power, RF signal, plasma parameter
- optical emission, OES, emission spectrum
- mass flow, gas flow, MFC
- SECS/GEM, SEMI EDA, Interface A, SVID, CEID

### 대표 사용 예

```text
플라즈마 챔버의 RF 신호와 OES 데이터를 이용해 공정 이상을 탐지
장비 로그와 센서 트레이스를 이용해 고장 원인을 진단
SECS/GEM으로 수집한 장비 상태 데이터를 이용해 예지보전 수행
```

## B-2. 공정 데이터

제조 공정의 조건, 이력, 레시피, 파라미터를 말한다.

### 포함하려는 데이터

- process data, manufacturing data, fabrication data
- process history, wafer history, lot history
- run data, run history
- recipe, process recipe, equipment recipe
- process condition, process parameter, control parameter
- setpoint, target value, process variable
- process drift, process excursion
- APC, SPC, FDC, R2R, run-to-run

### 대표 사용 예

```text
공정 레시피와 웨이퍼 이력을 이용해 수율을 예측
런투런 데이터를 이용해 다음 공정 조건을 보정
공정 파라미터와 검사 결과를 연결해 레시피를 최적화
```

## B-3. 검사/계측/결과 데이터

공정 이후 웨이퍼, 기판, 패널, 글라스에서 얻은 결과 데이터를 말한다.

### 포함하려는 데이터

- inspection result, metrology result, measurement result
- wafer inspection, substrate inspection, panel inspection
- defect inspection, e-beam inspection, SEM inspection
- wafer metrology, inline metrology, optical metrology
- CD-SEM, overlay metrology, film metrology
- wafer sort, wafer test, wafer probe, WAT, PCM
- defect map, wafer defect map, defect image
- wafer map, bin map, yield map, failure map
- yield data, yield loss, yield analysis
- CD variation, overlay error, film thickness, etch depth

### 대표 사용 예

```text
웨이퍼맵을 딥러닝으로 분류
SEM 결함 이미지를 이용해 자동 결함 분류
오버레이 계측 데이터를 이용해 다음 노광 조건을 보정
수율맵과 공정 이력을 연결해 수율 저하 원인을 분석
```

## C. AI 분석/진단/예측/제어 영역

이 영역은 “AI/ML이 실제로 사용되는가?”를 확인하는 관문이다.

V3에서는 `AI`라는 단어 하나만으로는 약하다고 보고, AI가 수행하는 기능까지 드러나는 표현을 중심으로 구성했다.

## C-1. AI/ML 일반 기술

### 포함하려는 표현

- artificial intelligence, AI-based, AI-assisted
- machine learning, ML-based
- deep learning, DL-based
- neural network, DNN, CNN, RNN
- transformer
- trained model, learning model, prediction model
- feature extraction, feature learning
- pattern recognition

## C-2. 이상탐지/고장진단

### 포함하려는 기능

- anomaly detection
- abnormality detection
- outlier detection
- drift detection
- fault detection
- fault classification
- fault diagnosis
- failure prediction
- root cause analysis

### 대표 사용 예

```text
챔버 센서 데이터로 장비 이상을 탐지
공정 로그로 고장 원인을 분석
플라즈마 신호로 공정 드리프트를 탐지
```

## C-3. 결함 검출/결함 분류

### 포함하려는 기능

- defect detection
- defect classification
- defect recognition
- defect identification
- automatic defect classification
- automatic defect review

### 대표 사용 예

```text
SEM 이미지를 이용한 결함 자동 분류
웨이퍼 결함맵을 이용한 결함 패턴 식별
검사 이미지에서 nuisance defect와 killer defect 분리
```

## C-4. 가상계측/결과 예측

### 포함하려는 기능

- virtual metrology
- soft sensor
- inferential measurement
- yield prediction
- defect prediction
- CD prediction
- overlay prediction
- film thickness prediction
- endpoint prediction

### 대표 사용 예

```text
공정 중 센서 데이터로 실제 계측값을 예측
검사를 하지 않은 웨이퍼의 CD 값을 가상계측
공정 데이터 기반으로 수율 또는 결함 확률을 예측
```

## C-5. 공정 제어/레시피 최적화

### 포함하려는 기능

- process control
- equipment control
- chamber control
- advanced process control
- run-to-run control
- model predictive control
- process optimization
- recipe optimization
- parameter optimization
- process recommendation
- recipe recommendation

### 대표 사용 예

```text
AI가 다음 공정의 레시피를 추천
이전 웨이퍼 결과를 이용해 다음 런의 공정 조건을 보정
수율을 높이도록 공정 파라미터를 최적화
```

## C-6. 예지보전/디지털트윈

### 포함하려는 기능

- predictive maintenance
- condition-based maintenance
- remaining useful life
- digital twin
- virtual fab
- virtual manufacturing
- surrogate model

### 대표 사용 예

```text
장비 센서 데이터로 부품 잔여수명을 예측
가상 팹 모델로 공정 조건 변경의 결과를 예측
디지털트윈으로 장비 상태와 공정 결과를 시뮬레이션
```

## D. 제외 영역

이 영역은 V2 상위 200개에서 실제로 많이 유입된 노이즈를 줄이기 위한 `NOT` 조건이다.

## 제외하려는 문헌

### 의료/바이오

- medical image, MRI, ultrasound, endoscope
- biomarker, cancer, dementia, retina, heart, brain
- 의료영상, 환자, 질병, 바이오마커, 수술

제외 이유: `diagnosis`, `image`, `AI`, `classification` 때문에 많이 들어왔지만 A11 제조 데이터와 무관하다.

### 차량/모빌리티/HMD

- vehicle, automotive, aircraft, drone
- head-up display, head-mounted display
- gaze tracking, AR, VR
- 차량, 자동차, 항공기, 드론, 시선추적

제외 이유: `display`, `control`, `prediction`, `AI` 때문에 들어왔지만 반도체 제조와 무관하다.

### 일반 UI/영상/소프트웨어

- graphical user interface, display interface
- image forming apparatus
- video highlight
- cybersecurity, vulnerability, project management

제외 이유: AI/영상/제어 문맥은 있지만 제조 장비/공정 데이터가 아니다.

### 배터리/에너지

- rechargeable battery, secondary battery, battery pack
- negative electrode, separator
- fuel cell

제외 이유: 결함 검사, 수율, 소재 제조 문맥이 있어도 A11의 반도체 제조 범위와 다르다.

단, A11 문제 범위에 솔라셀/태양전지는 포함될 수 있으므로 `solar cell manufacturing`, `photovoltaic process`는 살리고, 일반 `solar power generation system`은 제외했다.

## 의도적으로 뺀 단독어

아래 단어들은 A11 핵심 특허에도 나올 수 있지만, 실제 WIPS 결과에서는 노이즈를 훨씬 많이 끌어왔다.

```text
display
display device
display panel
substrate
AI
ML
control
prediction
estimate
diagnosis
analysis
optimization
model
inspection
metrology
image
sensor
temperature
pressure
defect
yield
data
```

V3에서는 이런 단어를 단독으로 쓰지 않고, 가능한 한 아래처럼 복합 표현으로 제한했다.

```text
wafer inspection
process data
chamber pressure
defect classification
yield prediction
process optimization
recipe optimization
display manufacturing
substrate processing
```

## V3가 찾고 싶은 대표 특허

- 웨이퍼맵을 딥러닝으로 분류/예측하는 특허
- 챔버 센서 로그로 플라즈마 공정 이상을 탐지하는 특허
- 계측 결과로 CD, overlay, 막두께를 예측하는 가상계측 특허
- 결함 이미지를 ML로 자동 분류하는 검사 장비 특허
- 공정 레시피를 AI로 추천/최적화하는 특허
- 반도체 장비 상태 데이터로 고장진단/예지보전을 하는 특허
- 디지털트윈이나 가상 팹으로 공정 결과를 예측하는 특허

## V3가 덜 잡으려는 문헌

- 단순 표시장치 구동회로
- 일반 의료 AI 진단
- 차량 디스플레이 제어
- 일반 이미지 처리/GUI
- 배터리 결함 검사
- 일반 소프트웨어 AI
- 반도체 재료 조성만 있고 AI 데이터 분석이 없는 특허

## 성능 판정 기준

V3 검색 후 상위 200개를 다시 확인했을 때 아래 기준으로 본다.

- A11 확실 + 후보가 40건 이상: 실사용 가능
- A11 확실 + 후보가 25~39건: 아직 넓지만 분석 가능
- A11 확실 + 후보가 25건 미만: 여전히 노이즈가 많거나 검색식이 핵심을 제대로 못 잡는 상태

V3가 너무 좁아져서 결과가 부족하면, `semiconductor wafer`, `processed substrate`, `display inspection`, `display metrology`, `solar cell result`, `data-driven`, `predictive` 같은 표현을 일부 복원한다.

