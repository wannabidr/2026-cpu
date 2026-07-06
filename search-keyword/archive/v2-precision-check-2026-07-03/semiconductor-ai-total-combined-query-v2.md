# V2 - A11 반도체 제조 AI 특허 검색식

이 파일은 A11 과제인 **A.I를 이용한 반도체 장치**에 맞게 V1 초광역 검색식을 정밀화한 버전이다.

V1은 누락 방지 목적의 Raw 검색식이었고, 실제 WIPS ON 검색 결과에서 배터리, 농업, 바이오마커, 일반 가스센서, 일반 기계 진단 등 A11과 무관한 문헌이 대량 유입되었다. V2에서는 다음 3개 조건을 모두 만족하도록 검색 구조를 바꾼다.

1. 반도체, 디스플레이, 솔라 제조/공정/장비/기판 문맥
2. 장비 데이터, 공정 데이터, 기판/웨이퍼/글라스/패널 결과 데이터 수집 또는 계측 문맥
3. AI/ML 기반 분석, 진단, 예측, 제어, 최적화 문맥

중국은 WIPS 국가 필터에서 제외해서 보는 현재 운용을 전제로 한다.

## V2 핵심 변경점

- `G01N%`, `G01B%`, `G01R%`, `G01J%`, `G01M%`, `G05B%`, `G16Y%` 같은 일반 측정/제어/IoT 분류를 반도체 조건 블록에서 제거했다.
- 일반어인 `device`, `system`, `sensor`, `data`, `control`, `smart`, `automated`가 단독으로 A11 조건을 통과하지 못하게 했다.
- 반도체/디스플레이/솔라 제조 문맥을 먼저 강제한 뒤, 데이터 수집/결과 데이터와 AI 분석/진단/제어 조건을 각각 AND로 묶었다.
- 제목만 반도체인 설계 자동화, 표시장치 구동회로, 일반 센서 제조 특허가 들어오지 않도록 제조 데이터/공정 데이터/결과 데이터 조건을 별도 블록으로 분리했다.

## 1. V2 전체 통합 검색식

```markdown
(
  (
    H01L21% OR H01L22% OR H01L21/02% OR H01L21/66% OR H01L21/67% OR H01L21/672%
    OR H01L21/67242 OR H01L21/67276
    OR H01L22/10% OR H01L22/12% OR H01L22/20% OR H01L22/26% OR H01L22/34%
    OR H10P% OR H10B% OR H10D% OR H10F% OR H10H% OR H10K% OR H10N%
    OR G03F1% OR G03F7% OR G03F9%
    OR B24B37%
    OR C23C14% OR C23C16% OR C23C18%
    OR H01J37/28% OR H01J37/32%
    OR H01L31% OR H01L27% OR G02F1%
  ).IPCM,IPC,CPCM,CPC.
  OR
  (
    semiconductor% OR "semi-conductor%" OR "semiconductor manufacturing" OR "semiconductor fabrication"
    OR "semiconductor processing" OR "semiconductor process%" OR "semiconductor production"
    OR "semiconductor equipment" OR "semiconductor manufacturing equipment"
    OR "semiconductor processing apparatus" OR "semiconductor processing system"
    OR "semiconductor device manufacturing" OR "semiconductor device fabrication"

    OR wafer% OR "semiconductor wafer%" OR "silicon wafer%" OR "processed wafer%"
    OR "wafer manufacturing" OR "wafer fabrication" OR "wafer processing"
    OR "wafer process%" OR "wafer inspection" OR "wafer metrology" OR "wafer test"
    OR "wafer map" OR "wafer defect map" OR "wafer result%"

    OR substrate% OR "semiconductor substrate%" OR "target substrate%" OR "processed substrate%"
    OR "substrate processing" OR "substrate processing apparatus" OR "substrate processing system"
    OR "substrate inspection" OR "substrate metrology"

    OR "process chamber%" OR "processing chamber%" OR "etch chamber%" OR "deposition chamber%"
    OR "plasma chamber%" OR "reaction chamber%" OR "vacuum chamber%" OR "transfer chamber%"
    OR "load lock" OR "load-lock" OR "processing module%" OR "process module%"

    OR etch OR etching OR "plasma etching" OR "dry etching" OR "wet etching"
    OR "reactive ion etching" OR RIE OR "atomic layer etching" OR ALE
    OR deposition OR "thin film deposition" OR CVD OR "chemical vapor deposition"
    OR PECVD OR LPCVD OR MOCVD OR ALD OR "atomic layer deposition"
    OR PVD OR sputter OR sputtering OR epitaxy OR epitaxial
    OR lithography OR photolithography OR exposure OR scanner OR "exposure apparatus"
    OR overlay OR alignment OR "critical dimension" OR "CD-SEM" OR CDSEM
    OR CMP OR "chemical mechanical polishing" OR "chemical mechanical planarization"
    OR polishing OR planarization OR cleaning OR "wet cleaning" OR anneal OR annealing
    OR oxidation OR diffusion OR implantation OR "ion implantation"

    OR display OR "display device%" OR "display panel%" OR "display manufacturing"
    OR "display fabrication" OR "panel manufacturing" OR "panel fabrication"
    OR "glass substrate%" OR "TFT array" OR "thin film transistor array"
    OR OLED OR "organic light emitting" OR LCD OR "liquid crystal display"

    OR "solar cell%" OR "solar module%" OR "solar panel%" OR photovoltaic% OR "photo-voltaic%"
    OR "PV cell%" OR "photovoltaic device%" OR "photovoltaic module%"
    OR "perovskite solar cell%" OR "thin film solar cell%"

    OR 반도체 OR 반도체제조 OR "반도체 제조" OR 반도체공정 OR "반도체 공정"
    OR 반도체장비 OR "반도체 장비" OR 반도체소자제조 OR "반도체 소자 제조"
    OR 웨이퍼 OR 웨이퍼제조 OR "웨이퍼 제조" OR 웨이퍼공정 OR "웨이퍼 공정"
    OR 웨이퍼검사 OR "웨이퍼 검사" OR 웨이퍼계측 OR "웨이퍼 계측" OR 웨이퍼맵
    OR 기판 OR 기판처리 OR "기판 처리" OR 기판공정 OR "기판 공정"
    OR 공정챔버 OR "공정 챔버" OR 처리챔버 OR "처리 챔버"
    OR 식각 OR 증착 OR 노광 OR 리소그래피 OR 포토리소그래피
    OR 오버레이 OR 정렬 OR 임계치수 OR 선폭 OR 박막 OR 패터닝
    OR 화학기계연마 OR 연마 OR 평탄화 OR 세정 OR 열처리 OR 산화 OR 확산 OR 이온주입
    OR 디스플레이제조 OR "디스플레이 제조" OR 디스플레이공정 OR "디스플레이 공정"
    OR 표시장치제조 OR "표시장치 제조" OR 디스플레이패널 OR "디스플레이 패널"
    OR 글라스기판 OR "글라스 기판" OR 유리기판 OR "유리 기판"
    OR 태양전지 OR "태양 전지" OR 태양전지제조 OR "태양 전지 제조"
    OR 솔라셀 OR "솔라 셀" OR 광전지 OR 태양광모듈 OR "태양광 모듈"

    OR 半導体 OR 半導体製造 OR "半導体 製造" OR 半導体プロセス OR "半導体 プロセス"
    OR 半導体装置 OR 半導体デバイス OR ウェハ OR ウエハ OR ウェーハ
    OR ウェハ処理 OR ウエハ処理 OR ウェーハ処理 OR 基板処理
    OR エッチング OR 成膜 OR 露光 OR リソグラフィ OR CMP OR 洗浄
    OR ディスプレイ製造 OR 表示装置 OR ガラス基板 OR 太陽電池

    OR 半导体 OR 半導體 OR 半导体制造 OR 半導體製造
    OR 半导体工艺 OR 半導體製程 OR 晶圆 OR 晶圓 OR 晶圆处理 OR 晶圓處理
    OR 基板处理 OR 基板處理 OR 刻蚀 OR 蝕刻 OR 沉积 OR 沉積 OR 光刻 OR 微影
    OR 显示器制造 OR 顯示器製造 OR 显示面板 OR 顯示面板 OR 玻璃基板
    OR 太阳能电池 OR 太陽能電池 OR 光伏 OR 光電
  ).TI,AB,CL.
)
AND
(
  (
    "equipment data" OR "tool data" OR "chamber data" OR "machine data"
    OR "equipment log%" OR "tool log%" OR "process log%" OR "event log%"
    OR "sensor data" OR "sensor signal%" OR "process signal%" OR "in-situ signal%" OR "in situ signal%"
    OR "trace data" OR "process trace" OR "process trace data" OR "sensor trace" OR "equipment trace" OR "tool trace"
    OR "time series" OR "time-series" OR "temporal data" OR telemetry
    OR "status data" OR "state data" OR "operating data" OR "operation data"
    OR pressure OR temperature OR "chamber pressure" OR "chamber temperature" OR "wafer temperature"
    OR voltage OR current OR impedance OR "RF power" OR "RF signal" OR "RF reflection"
    OR plasma OR "plasma parameter%" OR "plasma impedance"
    OR "optical emission" OR OES OR "emission spectrum" OR spectrum OR spectra
    OR "mass flow" OR "gas flow" OR "flow rate" OR MFC
    OR vacuum OR vibration OR acoustic OR "motor current" OR "valve position" OR "throttle valve" OR "pump speed"
    OR endpoint OR "end point" OR "end-point" OR "endpoint signal" OR "endpoint detection"
    OR "equipment data acquisition" OR "SEMI EDA" OR "Interface A" OR "SECS/GEM" OR SECS OR GEM OR GEM300
    OR SVID OR CEID OR "status variable" OR "collection event" OR "data collection plan" OR DCP

    OR 장비데이터 OR "장비 데이터" OR 툴데이터 OR "툴 데이터" OR 챔버데이터 OR "챔버 데이터"
    OR 장비로그 OR "장비 로그" OR 공정로그 OR "공정 로그" OR 이벤트로그 OR "이벤트 로그"
    OR 센서데이터 OR "센서 데이터" OR 센서신호 OR "센서 신호" OR 공정신호 OR "공정 신호"
    OR 트레이스데이터 OR "트레이스 데이터" OR 추적데이터 OR "추적 데이터"
    OR 시계열데이터 OR "시계열 데이터" OR 상태데이터 OR "상태 데이터" OR 운전데이터 OR "운전 데이터"
    OR 압력 OR 온도 OR 전압 OR 전류 OR 임피던스 OR 플라즈마 OR 광방출 OR 발광스펙트럼
    OR 질량유량 OR 가스유량 OR 유량 OR 진공 OR 진동 OR 음향 OR 모터전류
    OR 밸브위치 OR 스로틀밸브 OR 펌프속도 OR 엔드포인트 OR 종점
  )
  OR
  (
    "process data" OR "manufacturing data" OR "fabrication data" OR "production data"
    OR "process history" OR "manufacturing history" OR "wafer history" OR "lot history"
    OR "run data" OR "run history" OR "process record%"
    OR recipe OR recipes OR "process recipe%" OR "manufacturing recipe%" OR "tool recipe%" OR "equipment recipe%"
    OR "recipe parameter%" OR "recipe setting%" OR "recipe data"
    OR "process condition%" OR "processing condition%" OR "process parameter%" OR "control parameter%"
    OR "operating parameter%" OR setpoint OR "set point" OR "target value%" OR "process variable%"
    OR "process window" OR "process margin" OR "process variation" OR "process drift" OR "process excursion"
    OR APC OR "advanced process control" OR SPC OR "statistical process control"
    OR FDC OR "fault detection and classification"
    OR R2R OR "run-to-run" OR "run to run" OR feedforward OR "feed forward" OR feedback OR "closed loop" OR "closed-loop"

    OR 공정데이터 OR "공정 데이터" OR 제조데이터 OR "제조 데이터" OR 생산데이터 OR "생산 데이터"
    OR 공정이력 OR "공정 이력" OR 제조이력 OR "제조 이력" OR 웨이퍼이력 OR "웨이퍼 이력" OR 로트이력 OR "로트 이력"
    OR 런데이터 OR "런 데이터" OR 런이력 OR "런 이력" OR 공정기록 OR "공정 기록"
    OR 레시피 OR 공정레시피 OR "공정 레시피" OR 레시피파라미터 OR "레시피 파라미터"
    OR 공정조건 OR "공정 조건" OR 공정파라미터 OR "공정 파라미터" OR 제어파라미터 OR "제어 파라미터"
    OR 설정값 OR 목표값 OR 공정변수 OR "공정 변수"
    OR 공정창 OR "공정 창" OR 공정윈도우 OR "공정 윈도우" OR 공정편차 OR 공정드리프트 OR 공정일탈
    OR 공정제어 OR 고급공정제어 OR 통계공정제어 OR 고장검출분류 OR 런투런 OR "런 투 런" OR "런-투-런"
    OR 피드포워드 OR 피드백 OR 폐루프 OR 폐쇄루프
  )
  OR
  (
    "inspection result%" OR "metrology result%" OR "measurement result%" OR "test result%"
    OR "process result%" OR "processing result%" OR "manufacturing result%"
    OR "wafer result%" OR "substrate result%" OR "panel result%" OR "glass result%"
    OR inspection OR "wafer inspection" OR "substrate inspection" OR "panel inspection" OR "glass inspection"
    OR "defect inspection" OR "optical inspection" OR "e-beam inspection" OR "electron beam inspection"
    OR "SEM inspection" OR "defect review" OR ADR OR "automatic defect review"
    OR metrology OR "wafer metrology" OR "process metrology" OR "inline metrology" OR "in-line metrology"
    OR "in situ metrology" OR "in-situ metrology" OR "optical metrology" OR scatterometry OR ellipsometry
    OR reflectometry OR interferometry OR spectroscopy
    OR "CD-SEM" OR CDSEM OR "critical dimension SEM" OR "overlay metrology" OR "film metrology"
    OR "thickness measurement" OR "profile measurement" OR "electrical measurement"
    OR "parametric test" OR "parametric data" OR E-test OR "electrical test" OR "wafer sort" OR "wafer test"
    OR WAT OR "wafer acceptance test" OR PCM OR "process control monitor"
    OR "wafer probe" OR "probe test" OR "wafer-level test" OR "wafer level test"
    OR defect OR defects OR "defect data" OR "defect map" OR "wafer defect map" OR "defect image"
    OR "defect pattern" OR "defect signature" OR "defect classification" OR "defect detection"
    OR "killer defect" OR "nuisance defect" OR "systematic defect" OR "random defect" OR "pattern defect"
    OR particle OR particles OR contamination OR residue OR scratch OR void OR bridge OR bridging OR open OR short
    OR "line collapse" OR "pattern collapse" OR hotspot OR "lithography hotspot" OR "pattern hotspot"
    OR "EUV stochastic%" OR "stochastic defect%" OR "line break" OR "missing contact" OR "merged contact"
    OR image OR images OR "inspection image" OR "wafer image" OR "SEM image" OR "optical image"
    OR "wafer map" OR "bin map" OR "wafer bin map" OR WBM OR "failure map" OR "yield map" OR "spatial map"
    OR yield OR "yield data" OR "yield loss" OR "yield analysis" OR "yield management" OR "yield excursion"
    OR "critical dimension" OR CD OR "CD variation" OR "CD uniformity" OR linewidth OR "line width"
    OR LER OR LWR OR EPE OR "edge placement error" OR overlay OR "overlay error"
    OR "film thickness" OR thickness OR uniformity OR nonuniformity OR "etch depth" OR "etch rate" OR "removal rate"

    OR 검사결과 OR "검사 결과" OR 계측결과 OR "계측 결과" OR 측정결과 OR "측정 결과" OR 시험결과 OR "시험 결과"
    OR 공정결과 OR "공정 결과" OR 제조결과 OR "제조 결과" OR 웨이퍼결과 OR "웨이퍼 결과" OR 기판결과 OR "기판 결과"
    OR 패널결과 OR "패널 결과" OR 글라스결과 OR "글라스 결과"
    OR 검사 OR 웨이퍼검사 OR "웨이퍼 검사" OR 기판검사 OR "기판 검사" OR 패널검사 OR "패널 검사"
    OR 결함검사 OR "결함 검사" OR 광학검사 OR 전자빔검사 OR SEM검사 OR 결함리뷰 OR 자동결함리뷰
    OR 계측 OR 메트롤로지 OR 측정 OR 인라인계측 OR 광학계측 OR 산란계측 OR 타원계측
    OR 전기적측정 OR 파라메트릭테스트 OR 웨이퍼테스트 OR 웨이퍼프로브
    OR 결함 OR 불량 OR 결점 OR 결함데이터 OR "결함 데이터" OR 결함맵 OR 웨이퍼맵 OR 빈맵
    OR 결함이미지 OR 결함패턴 OR 결함시그니처 OR 결함분류 OR 결함검출 OR 결함탐지
    OR 파티클 OR 입자 OR 오염 OR 잔류물 OR 스크래치 OR 보이드 OR 브리지 OR 오픈 OR 쇼트
    OR 수율 OR 수율데이터 OR "수율 데이터" OR 수율손실 OR 수율분석 OR 수율관리 OR 수율일탈
    OR 임계치수 OR 선폭 OR 오버레이 OR 정렬오차 OR 두께 OR 막두께 OR 균일도 OR 비균일도 OR 식각깊이 OR 식각률 OR 제거율
  )
).TI,AB,CL.
AND
(
  (
    G06N% OR G06F18% OR G06V% OR G06T7%
  ).IPCM,IPC,CPCM,CPC.
  OR
  (
    "artificial intelligence" OR "artificial-intelligence" OR A.I OR AI
    OR "AI-based" OR "AI based" OR "AI assisted" OR "AI-assisted"
    OR "machine learning" OR "machine-learning" OR ML
    OR "deep learning" OR "deep-learning" OR DL
    OR "neural network%" OR "artificial neural network%" OR ANN OR "deep neural network%" OR DNN
    OR "learning model%" OR "trained model%" OR "training model%"
    OR "prediction model%" OR "predictive model%" OR "classification model%" OR "regression model%"
    OR "estimation model%" OR "diagnosis model%" OR "diagnostic model%" OR "control model%"
    OR "data driven" OR "data-driven" OR "data based" OR "data-based"
    OR "model training" OR "training data" OR "learning data" OR "feature extraction" OR "feature learning"
    OR "pattern recognition" OR "representation learning" OR embedding OR embeddings

    OR anomaly OR "anomaly detection" OR abnormal OR abnormality OR "abnormal detection"
    OR outlier OR "outlier detection" OR "novelty detection" OR "deviation detection" OR "change detection" OR "drift detection"
    OR fault OR "fault detection" OR "fault classification" OR "fault diagnosis" OR "fault isolation"
    OR failure OR "failure detection" OR "failure diagnosis" OR "failure prediction"
    OR diagnosis OR diagnostic OR diagnostics OR "root cause" OR "root cause analysis" OR RCA
    OR "cause analysis" OR "cause identification" OR "causal analysis" OR "causal inference"
    OR "defect detection" OR "defect classification" OR "defect recognition" OR "defect identification"
    OR ADC OR "automatic defect classification" OR ADR OR "automatic defect review"

    OR "virtual metrology" OR VM OR "virtual measurement" OR "soft sensor" OR "soft sensing"
    OR "inferential sensor" OR "inferential measurement" OR "proxy metrology"
    OR predict OR prediction OR predictive OR forecast OR forecasting
    OR estimate OR estimation OR infer OR inference
    OR "quality prediction" OR "quality estimation" OR "process result prediction" OR "process outcome prediction"
    OR "yield prediction" OR "yield estimation" OR "defect prediction" OR "defect probability"
    OR "critical dimension prediction" OR "CD prediction" OR "overlay prediction" OR "film thickness prediction"
    OR "endpoint prediction" OR "remaining useful life" OR RUL

    OR control OR "process control" OR "equipment control" OR "tool control" OR "chamber control" OR "fab control"
    OR "advanced process control" OR APC OR "run-to-run control" OR R2R
    OR "feedback control" OR "feedforward control" OR "closed-loop control" OR "real-time control"
    OR "model predictive control" OR MPC OR "predictive control" OR "adaptive control"
    OR optimization OR optimisation OR optimize OR optimise
    OR "process optimization" OR "process optimisation" OR "recipe optimization" OR "recipe optimisation"
    OR "parameter optimization" OR "condition optimization" OR "yield optimization"
    OR tuning OR "recipe tuning" OR "parameter tuning" OR "auto tuning" OR "self tuning"
    OR "corrective action" OR "process recommendation" OR "recipe recommendation" OR "control recommendation"
    OR "recipe generation" OR "condition generation"
    OR "predictive maintenance" OR "condition based maintenance" OR "condition-based maintenance"
    OR "digital twin" OR "virtual fab" OR "virtual manufacturing" OR "simulation model" OR "surrogate model"
    OR "physics-informed" OR "physics based" OR "physics-based"

    OR 인공지능 OR "인공 지능" OR AI OR 에이아이
    OR 기계학습 OR "기계 학습" OR 머신러닝 OR "머신 러닝"
    OR 딥러닝 OR "딥 러닝" OR 심층학습 OR "심층 학습"
    OR 신경망 OR "신경망" OR 뉴럴네트워크 OR "뉴럴 네트워크" OR 인공신경망 OR "인공 신경망"
    OR 학습모델 OR "학습 모델" OR 훈련모델 OR "훈련 모델" OR 예측모델 OR "예측 모델"
    OR 분류모델 OR "분류 모델" OR 회귀모델 OR "회귀 모델" OR 추정모델 OR "추정 모델" OR 진단모델 OR "진단 모델"
    OR 데이터기반 OR "데이터 기반" OR 데이터구동 OR "데이터 구동" OR 데이터드리븐 OR "데이터 드리븐"
    OR 특징추출 OR "특징 추출" OR 특징학습 OR "특징 학습" OR 패턴인식 OR "패턴 인식"
    OR 이상탐지 OR "이상 탐지" OR 이상검출 OR "이상 검출" OR 이상감지 OR "이상 감지"
    OR 비정상탐지 OR "비정상 탐지" OR 이상치탐지 OR "이상치 탐지" OR 드리프트탐지 OR "드리프트 탐지"
    OR 고장검출 OR "고장 검출" OR 고장탐지 OR "고장 탐지" OR 고장분류 OR "고장 분류" OR 고장진단 OR "고장 진단"
    OR 결함검출 OR "결함 검출" OR 결함탐지 OR "결함 탐지" OR 결함분류 OR "결함 분류" OR 자동결함분류 OR "자동 결함 분류"
    OR 원인분석 OR "원인 분석" OR 근본원인 OR "근본 원인" OR 인과분석 OR "인과 분석"
    OR 가상계측 OR "가상 계측" OR 가상측정 OR "가상 측정" OR 소프트센서 OR "소프트 센서"
    OR 예측 OR 예측모델 OR "예측 모델" OR 추정 OR 추정모델 OR "추정 모델"
    OR 품질예측 OR "품질 예측" OR 공정결과예측 OR "공정 결과 예측"
    OR 수율예측 OR "수율 예측" OR 결함예측 OR "결함 예측" OR 임계치수예측 OR "임계 치수 예측"
    OR 오버레이예측 OR "오버레이 예측" OR 막두께예측 OR "막 두께 예측" OR 엔드포인트예측 OR "엔드포인트 예측"
    OR 공정제어 OR "공정 제어" OR 장비제어 OR "장비 제어" OR 고급공정제어 OR "고급 공정 제어"
    OR 런투런제어 OR "런투런 제어" OR 피드백제어 OR "피드백 제어" OR 폐루프제어 OR "폐루프 제어"
    OR 모델예측제어 OR "모델 예측 제어" OR 예측제어 OR "예측 제어" OR 적응제어 OR "적응 제어"
    OR 최적화 OR 공정최적화 OR "공정 최적화" OR 레시피최적화 OR "레시피 최적화"
    OR 파라미터최적화 OR "파라미터 최적화" OR 조건최적화 OR "조건 최적화" OR 수율최적화 OR "수율 최적화"
    OR 레시피추천 OR "레시피 추천" OR 공정추천 OR "공정 추천" OR 조건추천 OR "조건 추천" OR 레시피생성 OR "레시피 생성"
    OR 예지보전 OR 예방보전 OR 예측정비 OR 잔여수명 OR 잔존수명
    OR 디지털트윈 OR "디지털 트윈" OR 가상팹 OR "가상 팹" OR 가상제조 OR "가상 제조" OR 공정시뮬레이터 OR "공정 시뮬레이터"

    OR 人工知能 OR 機械学習 OR 深層学習 OR ニューラルネットワーク
    OR 異常検知 OR 異常検出 OR 故障検知 OR 故障診断 OR 欠陥検出 OR 欠陥分類
    OR 仮想計測 OR 予測 OR 推定 OR 工程制御 OR プロセス制御 OR 最適化 OR レシピ最適化

    OR 人工智能 OR 人工智慧 OR 机器学习 OR 機器學習 OR 深度学习 OR 深度學習 OR 神经网络 OR 神經網路
    OR 异常检测 OR 異常檢測 OR 故障检测 OR 故障檢測 OR 故障诊断 OR 故障診斷
    OR 缺陷检测 OR 缺陷檢測 OR 缺陷分类 OR 缺陷分類
    OR 虚拟量测 OR 虛擬量測 OR 预测 OR 預測 OR 估计 OR 估計
    OR 工艺控制 OR 製程控制 OR 优化 OR 優化 OR 配方优化 OR 配方優化
  ).TI,AB,CL.
)
```

## 2. V2 결과가 아직 많을 때 쓰는 2차 축소식

위 V2 검색식 결과가 여전히 많으면, 전체 검색식 뒤에 아래 블록을 추가한다. 이 블록은 A11에서 중요한 “AI가 데이터를 분석/진단/제어/최적화한다”는 기능을 더 강하게 요구한다.

```markdown
AND
(
  "anomaly detection" OR "fault detection" OR "fault diagnosis"
  OR "defect detection" OR "defect classification"
  OR "virtual metrology" OR "yield prediction" OR "process result prediction"
  OR "process control" OR "recipe optimization" OR "process optimization"
  OR "predictive maintenance" OR "root cause analysis"
  OR 이상탐지 OR 고장진단 OR 결함검출 OR 결함분류
  OR 가상계측 OR 수율예측 OR 공정결과예측
  OR 공정제어 OR 레시피최적화 OR 공정최적화
  OR 예지보전 OR 원인분석
).TI,AB,CL.
```

## 3. V2에서도 노이즈가 남을 때의 선택적 제외식

1차 V2에서는 제외식을 바로 쓰지 않는다. 다만 배터리, 농업, 바이오, 일반 기계, 토목/에너지 계측 문헌이 계속 많으면 아래 블록을 추가한다.

```markdown
NOT
(
  "battery pack" OR "secondary battery" OR "fuel cell"
  OR agriculture OR agricultural OR farm OR drone
  OR biomarker OR biomarkers OR medical OR patient OR disease OR diagnosis of disease
  OR brain OR pulmonary OR fibrosis OR blood OR serum OR uric acid
  OR coal OR rock OR mining OR oilfield OR wellhead OR wind turbine
  OR tire OR tyre OR sewing machine OR construction OR building
  OR water monitoring OR water quality OR fermentation OR odor OR breathalyzer
  OR 배터리팩 OR 이차전지 OR 농업 OR 드론 OR 바이오마커 OR 질병 OR 환자 OR 혈액
  OR 석탄 OR 암석 OR 광산 OR 유전 OR 풍력 OR 타이어 OR 재봉틀 OR 건설 OR 수질 OR 발효
).TI,AB,CL.
```

주의: `solar cell`, `photovoltaic`, `display`, `glass substrate`는 A11 문제 범위에 포함될 수 있으므로 제외하지 않는다.

## 4. 판정 기준

검색 결과를 유효/노이즈로 나눌 때는 아래 기준을 쓴다.

### 유효 가능성이 높은 문헌

- 반도체/디스플레이/솔라 제조 장비의 센서 데이터, 로그, 트레이스, 상태 데이터를 수집한다.
- 공정 레시피, 공정 조건, 공정 파라미터, 런 이력, 로트 이력, 공정 이력을 이용한다.
- 웨이퍼/기판/글라스/패널의 검사, 계측, 결함, 수율, 웨이퍼맵, CD, 오버레이, 막두께, 균일도 결과를 이용한다.
- 위 데이터에 대해 AI/ML이 이상탐지, 고장진단, 결함분류, 가상계측, 수율예측, 공정제어, 레시피최적화, 예지보전, 원인분석을 수행한다.

### 제외 가능성이 높은 문헌

- 반도체 칩 설계 자동화만 다루고 제조 장비/공정/결과 데이터 분석이 없다.
- 표시장치 회로, 클럭 전송, 픽셀 구조처럼 디스플레이 제품 구조만 다루고 제조 데이터 AI 분석이 없다.
- 일반 센서, 일반 측정 장치, 일반 산업 기계 진단이지만 반도체/디스플레이/솔라 제조 문맥이 없다.
- 바이오마커, 의료 진단, 농업 관리, 배터리 상태 추정, 수질 모니터링처럼 A11 산업 범위 밖의 데이터 분석이다.

