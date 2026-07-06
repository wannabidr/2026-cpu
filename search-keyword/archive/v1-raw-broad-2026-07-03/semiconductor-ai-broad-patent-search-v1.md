# V1 - 반도체 제조 AI 특허 검색식 - 1차 넓은 검색용

이 문서는 반도체 제조/공정/장비/검사/계측/수율 영역에서 AI, 머신러닝, 지능화 기술이 적용된 특허를 넓게 수집하기 위한 검색식 초안이다.

1차 리서치에서는 누락 방지가 우선이므로 `NOT`은 최소화하고, 한글/영어/일본어/중국어 표현, 띄어쓰기, 하이픈, 약어, 단복수, 번역어 차이를 넓게 포함한다.

## 검색식 설계 원칙

- `AI 공통 AND AI 세부`처럼 AI 공통 블록을 필수 병목으로 두면, `machine learning`, `trained model`, `data-driven model`만 쓰고 `AI`를 쓰지 않는 영문 특허가 빠질 수 있다.
- 추천 구조는 `(반도체 분류/문헌 키워드) AND (반도체 제조 문맥) AND (AI 분류/AI 키워드)`이다.
- 특허 문헌은 같은 개념을 `wafer`, `substrate`, `workpiece`, `semiconductor wafer`, `target substrate`처럼 다르게 쓰므로 동의어를 과하게 넣는 편이 1차 검색에 유리하다.
- 한글은 붙여쓰기/띄어쓰기 모두 넣는다. 예: `반도체제조 OR "반도체 제조"`.
- 영어는 하이픈/비하이픈/띄어쓰기 변형을 모두 넣는다. 예: `"machine learning" OR "machine-learning"`.
- `%`는 기존 초안의 절단 검색 기호를 따른다. 사용하는 DB에서 `*`를 쓰면 `%`를 `*`로 바꾼다.
- 짧은 약어(`AI`, `ML`, `VM`, `IC`, `CD`, `EDA`)는 노이즈가 크다. 1차에서는 포함하되, 결과가 과도하면 약어 단독 검색을 제거하거나 문맥 블록과 근접연산으로 묶는다.
- 1차 검색에서는 강한 제외어를 바로 적용하지 않는다. AI 반도체 칩/가속기 특허가 너무 많이 섞일 때만 마지막의 선택적 제외 블록을 쓴다.

## 권장 통합 구조

```markdown
(
  SEMICONDUCTOR_CLASS
  OR SEMICONDUCTOR_CORE_TEXT
)
AND
(
  SEMICONDUCTOR_MANUFACTURING_CONTEXT
)
AND
(
  AI_CLASS
  OR AI_CORE_TEXT
  OR AI_FUNCTION_TEXT
  OR AI_ALGORITHM_TEXT
)
```

검색 DB가 사용자 정의 블록명을 지원하지 않으면, 아래 각 블록의 실제 괄호식을 위 구조에 치환해서 사용한다.

## 1. 반도체/제조 관련 분류코드

```markdown
(
  H01L21% OR H01L22% OR H01L21/02% OR H01L21/66% OR H01L21/67% OR H01L21/672%
  OR H01L21/67242 OR H01L21/67276
  OR H01L22/10% OR H01L22/12% OR H01L22/20% OR H01L22/26% OR H01L22/34%
  OR H10P% OR H10B% OR H10D% OR H10F% OR H10H% OR H10N%

  OR G03F1% OR G03F7% OR G03F9%
  OR B24B37%
  OR C23C14% OR C23C16% OR C23C18%
  OR H01J37/28% OR H01J37/32%

  OR G01N% OR G01B% OR G01R% OR G01J% OR G01M%
  OR G05B13% OR G05B19% OR G05B19/418 OR G05B23% OR G05B23/02% OR G05B23/0283
  OR G06Q10/063% OR G06Q10/0631%
  OR G16Y%
).IPCM,IPC,CPCM,CPC.
```

## 2. AI/패턴인식 관련 분류코드

```markdown
(
  G06N%
  OR G06F18% OR G06F17/18%
  OR G06V% OR G06T7%
).IPCM,IPC,CPCM,CPC.
```

## 3. 반도체 공통 텍스트 블록

```markdown
(
  semiconductor% OR "semi-conductor%" OR "semi conductor%"
  OR wafer% OR "semi-conductor wafer%" OR "semiconductor wafer%" OR "silicon wafer%"
  OR substrate% OR "semiconductor substrate%" OR "target substrate%" OR "processed substrate%"
  OR workpiece% OR "semiconductor workpiece%"
  OR die OR dies OR chip OR chips
  OR "integrated circuit%" OR "integrated-circuit%" OR IC OR "IC device%" OR "IC manufacturing"
  OR "semiconductor device%" OR "solid state device%" OR "solid-state device%"
  OR "microelectronic%" OR "micro-electronic%" OR microfabrication OR "micro-fabrication"

  OR "semiconductor manufacturing" OR "semiconductor manufacture" OR "semiconductor production"
  OR "semiconductor fabrication" OR "semiconductor processing"
  OR "wafer fabrication" OR "wafer fab" OR "wafer manufacturing" OR "wafer processing"
  OR "substrate processing" OR "substrate treatment" OR "semiconductor treatment"
  OR "chip manufacturing" OR "chip fabrication" OR "device manufacturing"
  OR "semiconductor process%" OR "wafer process%" OR "fabrication process%"
  OR fab OR fabs OR foundry OR foundries
  OR "front end" OR "front-end" OR FEOL
  OR "back end" OR "back-end" OR BEOL
  OR "middle of line" OR "middle-of-line" OR MOL
  OR "thin film%" OR patterning OR "process module%"

  OR 반도체 OR 반도체제조 OR "반도체 제조" OR 반도체공정 OR "반도체 공정"
  OR 반도체소자 OR "반도체 소자" OR 반도체장치 OR "반도체 장치"
  OR 웨이퍼 OR 웨이퍼제조 OR "웨이퍼 제조" OR 웨이퍼공정 OR "웨이퍼 공정"
  OR 기판 OR 기판처리 OR "기판 처리" OR 기판공정 OR "기판 공정"
  OR 집적회로 OR "집적 회로" OR 칩제조 OR "칩 제조"
  OR 팹 OR 반도체팹 OR "반도체 팹" OR 파운드리
  OR 전공정 OR "전 공정" OR 후공정 OR "후 공정" OR 중간공정 OR "중간 공정"
  OR 박막 OR 패터닝 OR 패턴형성 OR "패턴 형성"

  OR 半導体 OR 半導体製造 OR "半導体 製造" OR 半導体プロセス OR "半導体 プロセス"
  OR 半導体装置 OR "半導体 装置" OR 半導体デバイス OR "半導体 デバイス"
  OR ウェハ OR ウエハ OR ウェーハ OR 基板 OR 集積回路
  OR ウェハ製造 OR ウエハ製造 OR ウェーハ製造 OR ウェハ処理 OR ウエハ処理 OR ウェーハ処理
  OR ファブ OR ファウンドリ OR フロントエンド OR バックエンド

  OR 半导体 OR 半導體 OR 半导体制造 OR 半導體製造 OR "半导体 制造" OR "半導體 製造"
  OR 半导体工艺 OR 半導體製程 OR "半导体 工艺" OR "半導體 製程"
  OR 半导体器件 OR 半導體器件 OR 半导体装置 OR 半導體裝置
  OR 晶圆 OR 晶圓 OR 晶片 OR 基板
  OR 晶圆制造 OR 晶圓製造 OR 晶圆处理 OR 晶圓處理
  OR 集成电路 OR 積體電路 OR 集積電路
  OR 前道工艺 OR 前段製程 OR 后道工艺 OR 後段製程
)
```

## 4. 반도체 제조 문맥 블록

이 블록은 반도체 자체가 아니라 반도체 "제조/공정/장비/검사/계측/수율/운영" 문맥임을 잡기 위한 블록이다.

```markdown
(
  equipment OR equipments OR tool OR tools OR apparatus OR apparatuses OR device OR devices
  OR module OR modules OR system OR systems
  OR "process tool%" OR "processing tool%" OR "semiconductor equipment"
  OR "semiconductor manufacturing equipment" OR "fabrication equipment"
  OR "production equipment" OR "process equipment" OR "wafer processing equipment"
  OR "substrate processing apparatus" OR "substrate processing system"
  OR "semiconductor processing apparatus" OR "semiconductor processing system"

  OR chamber OR chambers OR "process chamber%" OR "processing chamber%"
  OR "etch chamber%" OR "deposition chamber%" OR "plasma chamber%" OR "reaction chamber%"
  OR reactor OR reactors OR "vacuum chamber%" OR "load lock" OR "load-lock"
  OR "transfer chamber%" OR "processing module%" OR "tool module%"
  OR "electrostatic chuck" OR ESC OR susceptor OR chuck

  OR etch OR etching OR "dry etch%" OR "wet etch%" OR "plasma etch%" OR "reactive ion etch%" OR RIE
  OR "atomic layer etch%" OR ALE
  OR deposition OR depositing OR "thin film deposition"
  OR CVD OR "chemical vapor deposition" OR "chemical vapour deposition"
  OR PECVD OR LPCVD OR MOCVD OR ALD OR "atomic layer deposition"
  OR PVD OR sputter OR sputtering OR evaporation OR epitaxy OR epitaxial
  OR lithography OR lithographic OR photolithography OR "photo lithography"
  OR exposure OR scanner OR "exposure apparatus" OR stepper
  OR focus OR dose OR "focus dose" OR "focus/dose"
  OR overlay OR "overlay error" OR alignment OR registration
  OR "critical dimension" OR CD OR "edge placement error" OR EPE
  OR "photoresist" OR resist OR coating OR coater OR developer OR "track apparatus"
  OR CMP OR "chemical mechanical polishing" OR "chemical mechanical planarization" OR "chemical mechanical planarisation"
  OR polishing OR planarization OR planarisation OR slurry OR pad OR "polishing pad" OR "removal rate"
  OR cleaning OR clean OR "wet cleaning" OR "dry cleaning" OR rinsing OR drying
  OR anneal OR annealing OR "thermal treatment" OR oxidation OR diffusion
  OR implantation OR "ion implantation" OR implanter OR doping OR dopant OR RTP OR "rapid thermal"

  OR process OR processes OR processing OR fabrication OR manufacture OR manufacturing
  OR "unit process%" OR "process step%" OR "processing step%" OR "process sequence%" OR "process flow%"
  OR "process integration" OR "integrated process%"
  OR recipe OR recipes OR "process recipe%" OR "manufacturing recipe%" OR "tool recipe%" OR "equipment recipe%"
  OR "recipe parameter%" OR "recipe setting%" OR "recipe data" OR "recipe optimization" OR "recipe optimisation"
  OR "process condition%" OR "processing condition%" OR "process parameter%" OR "control parameter%"
  OR "operating parameter%" OR "set point" OR setpoint OR "target value%" OR "target parameter%"
  OR "process variable%" OR "critical parameter%" OR "key parameter%"

  OR lot OR lots OR batch OR batches OR "wafer lot%" OR "lot history" OR "wafer history"
  OR "process history" OR "manufacturing history" OR "run data" OR "run history"
  OR "process record%" OR "historical data" OR "production data"
  OR "process trace" OR "process trace data" OR "event log%" OR "process log%" OR "equipment log%" OR "tool log%"
  OR "trace data" OR "sensor trace" OR "equipment trace" OR "tool trace"
  OR "golden trace" OR "golden run" OR "reference trace"
  OR "process signature" OR "equipment signature" OR "tool signature" OR "chamber signature"
  OR "tool fingerprint" OR "chamber fingerprint"

  OR sensor OR sensors OR "sensor data" OR "sensor signal%" OR signal OR signals
  OR waveform OR waveforms OR telemetry OR "time series" OR "time-series" OR "temporal data"
  OR "equipment data" OR "tool data" OR "chamber data" OR "machine data"
  OR "status data" OR "state data" OR "operating data" OR "operation data" OR "process signal%"
  OR "in-situ signal" OR "in situ signal" OR insitu
  OR pressure OR temperature OR voltage OR current OR impedance
  OR "RF power" OR "RF signal" OR "RF reflection" OR plasma OR "plasma parameter%" OR "plasma impedance"
  OR "optical emission" OR OES OR "emission spectrum" OR spectrum OR spectra
  OR "mass flow" OR "gas flow" OR "flow rate" OR MFC
  OR vacuum OR humidity OR vibration OR acoustic OR "motor current"
  OR "valve position" OR "throttle valve" OR "pump speed"
  OR endpoint OR "end point" OR "end-point" OR "endpoint signal" OR "endpoint detection"

  OR "equipment data acquisition" OR "SEMI EDA" OR "Interface A"
  OR "SECS/GEM" OR SECS OR GEM OR GEM300
  OR SVID OR CEID OR "status variable" OR "collection event"
  OR "data collection plan" OR DCP
  OR MES OR "manufacturing execution system"
  OR EAP OR "equipment automation" OR CIM OR "computer integrated manufacturing"
  OR APC OR "advanced process control"
  OR FDC OR "fault detection and classification"
  OR SPC OR "statistical process control"
  OR R2R OR "run-to-run" OR "run to run"
  OR feedforward OR "feed forward" OR "feed-forward"
  OR feedback OR "feed back" OR "closed loop" OR "closed-loop"
  OR "model predictive control" OR MPC

  OR inspection OR inspect OR inspecting OR metrology OR measurement OR measuring
  OR "wafer inspection" OR "substrate inspection" OR "defect inspection"
  OR "optical inspection" OR "e-beam inspection" OR "electron beam inspection"
  OR "SEM inspection" OR "SEM review" OR "defect review"
  OR ADR OR "automatic defect review" OR ADC OR "automatic defect classification"
  OR "inline metrology" OR "in-line metrology" OR "in situ metrology" OR "in-situ metrology"
  OR "optical metrology" OR scatterometry OR ellipsometry OR reflectometry OR interferometry OR spectroscopy
  OR "CD-SEM" OR CDSEM OR "critical dimension SEM"
  OR "overlay metrology" OR "film metrology" OR "thickness measurement"
  OR "electrical measurement" OR "parametric test" OR "parametric data"
  OR E-test OR "electrical test" OR "wafer sort" OR "wafer test"
  OR WAT OR "wafer acceptance test" OR PCM OR "process control monitor"
  OR "wafer probe" OR "probe test" OR "wafer-level test" OR "wafer level test"

  OR defect OR defects OR defective OR "defect data" OR "defect map" OR "wafer defect map"
  OR "defect image" OR "defect pattern" OR "defect signature"
  OR "defect classification" OR "defect detection" OR "killer defect" OR "nuisance defect"
  OR "systematic defect" OR "random defect" OR "pattern defect" OR "process defect"
  OR particle OR particles OR contamination OR scratch OR void OR bridge OR bridging OR open OR short
  OR residue OR missing OR deformation OR collapse OR "line collapse" OR "pattern collapse"
  OR hotspot OR "lithography hotspot" OR "pattern hotspot"
  OR "EUV stochastic%" OR "stochastic defect%"
  OR "line break" OR "missing contact" OR "merged contact" OR protrusion OR necking OR "micro bridge" OR microbridge

  OR image OR images OR imaging OR "inspection image" OR "wafer image" OR "substrate image"
  OR "SEM image" OR "electron microscope image" OR "optical image"
  OR "bright field" OR brightfield OR "dark field" OR darkfield
  OR "wafer map" OR "wafer maps" OR "bin map" OR "bin maps" OR "wafer bin map" OR WBM
  OR "failure map" OR "yield map" OR "spatial map" OR "heat map"
  OR "map pattern" OR "wafer pattern" OR "spatial distribution" OR "defect distribution"
  OR "spatial signature" OR "yield signature"

  OR yield OR yields OR "yield data" OR "yield loss" OR "yield improvement" OR "yield enhancement"
  OR "yield prediction" OR "yield estimation" OR "yield analysis" OR "yield management"
  OR "yield learning" OR "yield ramp" OR "yield excursion"
  OR "low yield" OR "bad wafer" OR "good wafer" OR "pass fail" OR "pass/fail"
  OR binning OR "bin data" OR "failure analysis" OR "fail bit" OR "bit fail" OR "fail pattern"

  OR "equipment state" OR "tool state" OR "chamber state" OR "equipment condition" OR "tool condition"
  OR "equipment health" OR "tool health" OR "health index" OR "health score" OR "health state"
  OR "health monitoring" OR "condition monitoring" OR "condition indicator"
  OR "equipment monitoring" OR "tool monitoring" OR "chamber monitoring"
  OR "equipment diagnosis" OR "tool diagnosis" OR "chamber diagnosis"
  OR "equipment fault" OR "tool fault" OR "chamber fault"
  OR "equipment anomaly" OR "tool anomaly" OR "chamber anomaly"
  OR malfunction OR failure OR degradation OR drift OR aging OR ageing
  OR "process drift" OR "tool drift" OR "chamber drift"
  OR "predictive maintenance" OR "preventive maintenance" OR "preventative maintenance"
  OR "condition based maintenance" OR "condition-based maintenance"
  OR "remaining useful life" OR RUL OR prognostic OR prognostics

  OR "data integration" OR "data fusion" OR "sensor fusion" OR multimodal OR "multi-modal"
  OR "multi source" OR "multi-source" OR "heterogeneous data" OR "combined data"
  OR upstream OR downstream OR "cross process" OR "cross-process" OR "cross tool" OR "cross-tool"
  OR genealogy OR "wafer genealogy" OR "lot genealogy" OR "process genealogy"
  OR "digital twin" OR "digital twins" OR "virtual fab" OR "virtual factory" OR "virtual manufacturing"
  OR "process simulator" OR "fab simulator" OR "equipment simulator" OR "simulation model"
  OR "surrogate model" OR "hybrid model" OR "physics-informed" OR "physics based" OR "physics-based"
  OR scheduling OR dispatching OR routing OR "lot dispatching" OR "wafer dispatching"
  OR "tool selection" OR "route selection" OR WIP OR "work in process"
  OR "cycle time" OR throughput OR "through-put" OR bottleneck OR "capacity planning"
  OR "equipment utilization" OR utilization OR "load balancing" OR "line balancing"

  OR 공정장비 OR 제조장비 OR 반도체장비 OR 처리장치 OR 기판처리장치 OR 공정챔버 OR 챔버
  OR 식각장비 OR 증착장비 OR 노광장비 OR 세정장비 OR 연마장비 OR 계측장비 OR 검사장비
  OR 센서 OR 센서데이터 OR "센서 데이터" OR 센서신호 OR "센서 신호"
  OR 장비데이터 OR "장비 데이터" OR 공정데이터 OR "공정 데이터" OR 장비로그 OR "장비 로그"
  OR 공정로그 OR "공정 로그" OR 추적데이터 OR "추적 데이터" OR 트레이스데이터 OR "트레이스 데이터"
  OR 상태데이터 OR "상태 데이터" OR 시계열데이터 OR "시계열 데이터" OR 공정신호 OR "공정 신호"
  OR 압력 OR 온도 OR 전압 OR 전류 OR 임피던스 OR 플라즈마 OR 광방출 OR 발광스펙트럼
  OR 질량유량 OR 가스유량 OR 유량 OR 진공 OR 습도 OR 진동 OR 음향 OR 모터전류
  OR 밸브위치 OR 스로틀밸브 OR 펌프속도 OR 엔드포인트 OR 종점

  OR 공정 OR 제조공정 OR 웨이퍼공정 OR 단위공정 OR 공정단계 OR 공정흐름
  OR 레시피 OR 공정레시피 OR 공정조건 OR 공정파라미터 OR 제어파라미터
  OR 설정값 OR 목표값 OR 공정변수 OR 로트 OR 배치 OR 로트이력 OR 웨이퍼이력
  OR 공정이력 OR 제조이력 OR 런데이터 OR 런이력
  OR 공정제어 OR 고급공정제어 OR 통계공정제어 OR 공정모니터링
  OR 고장검출분류 OR 고장검출및분류 OR 런투런 OR "런 투 런" OR "런-투-런"
  OR 피드백 OR 피드포워드 OR 폐루프 OR 폐쇄루프 OR 모델예측제어
  OR 식각 OR 증착 OR 리소그래피 OR 노광 OR 오버레이 OR 정렬 OR 현상 OR 코팅
  OR 화학기계연마 OR CMP OR 연마 OR 평탄화 OR 세정 OR 열처리 OR 산화 OR 확산 OR 이온주입

  OR 검사 OR 웨이퍼검사 OR "웨이퍼 검사" OR 결함검사 OR "결함 검사"
  OR 광학검사 OR 전자빔검사 OR SEM검사 OR 결함리뷰 OR 자동결함리뷰
  OR 계측 OR 메트롤로지 OR 측정 OR 인라인계측 OR 광학계측
  OR 전기적측정 OR 파라메트릭테스트 OR 웨이퍼테스트 OR 웨이퍼프로브
  OR 결함 OR 불량 OR 결점 OR 결함맵 OR 웨이퍼맵 OR 빈맵 OR 불량맵
  OR 결함이미지 OR 결함패턴 OR 결함시그니처 OR 결함분류 OR 결함검출 OR 결함탐지
  OR 파티클 OR 입자 OR 오염 OR 잔류물 OR 브리지 OR 오픈 OR 쇼트
  OR 수율 OR 수율데이터 OR 수율손실 OR 수율향상 OR 수율예측 OR 수율분석 OR 수율관리
  OR 임계치수 OR 선폭 OR 오버레이 OR 정렬오차 OR 두께 OR 막두께 OR 균일도 OR 비균일도

  OR 장비상태 OR "장비 상태" OR 툴상태 OR "툴 상태" OR 챔버상태 OR "챔버 상태"
  OR 장비건전성 OR "장비 건전성" OR 장비상태진단 OR "장비 상태 진단"
  OR 장비진단 OR 장비이상 OR 장비고장 OR 고장진단 OR 이상진단
  OR 예지보전 OR 예방보전 OR 예측정비 OR 잔여수명 OR 잔존수명
  OR 챔버매칭 OR 장비매칭 OR 툴매칭 OR 보정 OR 캘리브레이션

  OR 데이터융합 OR 데이터통합 OR 센서융합 OR 다중데이터 OR 이종데이터
  OR 팹 OR 반도체팹 OR 제조라인 OR 생산라인 OR 스마트팩토리 OR 스마트팹
  OR 지능형팹 OR 디지털팹 OR 자율팹 OR 가상팹
  OR 제조실행시스템 OR 공정제어시스템 OR 수율관리시스템
  OR 디지털트윈 OR 가상모델 OR 공정시뮬레이터 OR 팹시뮬레이터
  OR 스케줄링 OR 디스패칭 OR 라우팅 OR 장비선택 OR 경로선택

  OR 製造装置 OR 処理装置 OR プロセス装置 OR チャンバ OR プロセスチャンバ
  OR センサ OR センサデータ OR 装置データ OR ログ OR トレースデータ
  OR 工程 OR プロセス OR レシピ OR プロセス条件 OR プロセスパラメータ
  OR エッチング OR 成膜 OR 露光 OR リソグラフィ OR CMP OR 洗浄 OR 熱処理 OR イオン注入
  OR 検査 OR 計測 OR 欠陥 OR 欠陥検出 OR 欠陥分類 OR ウェハマップ OR 歩留まり OR 歩留り
  OR 異常検知 OR 故障検知 OR 故障診断 OR 予知保全 OR 予防保全
  OR デジタルツイン OR スケジューリング OR ディスパッチング

  OR 制造设备 OR 製造設備 OR 处理装置 OR 處理裝置 OR 工艺腔室 OR 製程腔室
  OR 传感器 OR 感測器 OR 传感器数据 OR 感測器資料 OR 设备数据 OR 設備資料
  OR 工艺数据 OR 製程資料 OR 日志 OR 轨迹数据 OR 軌跡資料
  OR 工艺 OR 製程 OR 配方 OR 工艺配方 OR 製程配方 OR 工艺参数 OR 製程參數
  OR 刻蚀 OR 蝕刻 OR 沉积 OR 沉積 OR 曝光 OR 光刻 OR 微影 OR CMP OR 清洗 OR 清潔 OR 热处理 OR 熱處理
  OR 检测 OR 檢測 OR 检查 OR 檢查 OR 量测 OR 量測 OR 缺陷 OR 瑕疵
  OR 缺陷检测 OR 缺陷檢測 OR 缺陷分类 OR 缺陷分類 OR 晶圆图 OR 晶圓圖
  OR 良率 OR 良率预测 OR 良率預測 OR 故障检测 OR 故障檢測 OR 异常检测 OR 異常檢測
  OR 预测性维护 OR 預測性維護 OR 数字孪生 OR 數位孿生 OR 调度 OR 調度
)
```

## 5. AI 공통 텍스트 블록

```markdown
(
  "artificial intelligence" OR "artificial-intelligence" OR "machine intelligence"
  OR AI OR "AI-based" OR "AI based" OR "AI assisted" OR "AI-assisted"
  OR intelligent OR intelligence OR smart OR automated OR automation OR autonomous OR autonomy
  OR "machine learning" OR "machine-learning" OR ML
  OR "statistical learning" OR "statistical model%"
  OR "deep learning" OR "deep-learning" OR DL
  OR "neural network%" OR "artificial neural network%" OR ANN
  OR "deep neural network%" OR DNN
  OR "learning model%" OR "trained model%" OR "training model%"
  OR "prediction model%" OR "predictive model%" OR "classification model%" OR "classifier"
  OR "regression model%" OR "estimation model%" OR "diagnosis model%" OR "diagnostic model%"
  OR "control model%" OR "optimization model%" OR "optimisation model%"
  OR "data driven" OR "data-driven" OR "data based" OR "data-based" OR "data centric" OR "data-centric"
  OR "model training" OR "training data" OR "learning data" OR "labeled data" OR "labelled data"
  OR "feature extraction" OR "feature generation" OR "feature engineering" OR "feature selection"
  OR "feature learning" OR "representation learning" OR embedding OR embeddings
  OR "pattern recognition" OR "pattern learning" OR "predictive analytics" OR "advanced analytics"
  OR "adaptive model%" OR "intelligent model%" OR "self learning" OR "self-learning"

  OR 인공지능 OR "인공 지능" OR AI OR 지능형 OR 지능화 OR 스마트 OR 자동화 OR 자율화
  OR 기계학습 OR "기계 학습" OR 머신러닝 OR "머신 러닝"
  OR 통계학습 OR "통계 학습" OR 통계모델 OR "통계 모델"
  OR 딥러닝 OR "딥 러닝" OR 심층학습 OR "심층 학습"
  OR 신경망 OR "신경 망" OR 뉴럴네트워크 OR "뉴럴 네트워크"
  OR 인공신경망 OR "인공 신경망" OR 심층신경망 OR "심층 신경망"
  OR 학습모델 OR "학습 모델" OR 훈련모델 OR "훈련 모델" OR 학습된모델 OR "학습된 모델"
  OR 예측모델 OR "예측 모델" OR 분류모델 OR "분류 모델" OR 회귀모델 OR "회귀 모델"
  OR 추정모델 OR "추정 모델" OR 진단모델 OR "진단 모델" OR 제어모델 OR "제어 모델"
  OR 최적화모델 OR "최적화 모델"
  OR 데이터기반 OR "데이터 기반" OR 데이터구동 OR "데이터 구동" OR 데이터드리븐 OR "데이터 드리븐"
  OR 모델학습 OR "모델 학습" OR 모델훈련 OR "모델 훈련"
  OR 학습데이터 OR "학습 데이터" OR 훈련데이터 OR "훈련 데이터"
  OR 트레이닝데이터 OR "트레이닝 데이터" OR 라벨데이터 OR "라벨 데이터" OR 레이블데이터 OR "레이블 데이터"
  OR 특징추출 OR "특징 추출" OR 피처추출 OR "피처 추출"
  OR 특징학습 OR "특징 학습" OR 표현학습 OR "표현 학습" OR 임베딩
  OR 패턴인식 OR "패턴 인식" OR 예측분석 OR "예측 분석" OR 지능모델 OR "지능 모델"

  OR 人工知能 OR AI OR 知能化 OR スマート OR 自動化 OR 自律化
  OR 機械学習 OR マシンラーニング OR 統計学習
  OR 深層学習 OR ディープラーニング OR ニューラルネットワーク OR 神経網
  OR 学習モデル OR 訓練モデル OR 予測モデル OR 分類モデル OR 回帰モデル OR 推定モデル
  OR データ駆動 OR データドリブン OR 特徴抽出 OR 特徴学習 OR 表現学習 OR パターン認識

  OR 人工智能 OR 人工智慧 OR AI OR 智能化 OR 智慧化 OR 智能 OR 智慧 OR 自动化 OR 自動化 OR 自主化
  OR 机器学习 OR 機器學習 OR 机械学习 OR 機械學習 OR 统计学习 OR 統計學習
  OR 深度学习 OR 深度學習 OR 神经网络 OR 神經網路 OR 神經網絡
  OR 学习模型 OR 學習模型 OR 训练模型 OR 訓練模型
  OR 预测模型 OR 預測模型 OR 分类模型 OR 分類模型 OR 回归模型 OR 迴歸模型 OR 估计模型 OR 估計模型
  OR 数据驱动 OR 數據驅動 OR 資料驅動 OR 特征提取 OR 特徵提取 OR 表征学习 OR 表徵學習 OR 模式识别 OR 模式識別
)
```

## 6. AI 기능/응용 텍스트 블록

```markdown
(
  "anomaly detection" OR anomaly OR anomalies OR anomalous
  OR "abnormal detection" OR abnormal OR abnormality OR abnormalities
  OR "outlier detection" OR outlier OR outliers
  OR "novelty detection" OR "deviation detection" OR "change detection" OR "drift detection"
  OR "excursion" OR excursions OR "out of control" OR "out-of-control" OR OOC
  OR alarm OR alarms OR "false alarm" OR "alarm reduction"

  OR fault OR faults OR faulty OR "fault detection" OR "fault classification"
  OR "fault detection and classification" OR FDC
  OR "fault diagnosis" OR "fault diagnostic" OR "fault isolation" OR "fault identification"
  OR "fault prediction" OR "failure detection" OR "failure diagnosis" OR "failure prediction"
  OR "root cause" OR "root-cause" OR "root cause analysis" OR RCA
  OR "cause analysis" OR "cause identification" OR "cause estimation" OR "causal diagnosis"
  OR troubleshooting OR "trouble shooting"

  OR "defect detection" OR "defect classification" OR "defect recognition" OR "defect identification"
  OR "automatic defect classification" OR ADC OR "automatic defect review" OR ADR
  OR "wafer defect pattern" OR "defect pattern classification"
  OR "wafer map classification" OR "bin map classification"

  OR "virtual metrology" OR VM OR "virtual measurement" OR "virtual measuring"
  OR "soft sensor" OR "soft sensing" OR "inferential sensor" OR "inferential measurement"
  OR "proxy metrology" OR "estimated metrology" OR "metrology prediction" OR "metrology estimation"
  OR predict OR predicts OR predicted OR predicting OR prediction OR predictive
  OR forecast OR forecasts OR forecasting
  OR estimate OR estimates OR estimated OR estimating OR estimation
  OR infer OR infers OR inferred OR inference
  OR "quality prediction" OR "quality estimation"
  OR "process result prediction" OR "process outcome prediction" OR "manufacturing result prediction"
  OR "yield prediction" OR "yield estimation" OR "yield forecasting"
  OR "defect prediction" OR "defect probability" OR "defect density prediction"
  OR "critical dimension prediction" OR "CD prediction" OR "overlay prediction" OR "film thickness prediction"
  OR "endpoint prediction" OR "endpoint estimation" OR "remaining time prediction"
  OR "remaining useful life" OR RUL OR "life prediction" OR "maintenance prediction"

  OR control OR controls OR controlled OR controlling
  OR "process control" OR "manufacturing control" OR "quality control" OR "yield control"
  OR "equipment control" OR "tool control" OR "chamber control" OR "fab control"
  OR "run-to-run control" OR "feedback control" OR "feedforward control"
  OR "closed-loop control" OR "real-time control" OR "in-situ control" OR "in situ control"
  OR "model predictive control" OR MPC OR "predictive control" OR "adaptive control"
  OR "optimal control" OR "robust control" OR "multivariable control" OR "control algorithm"
  OR optimization OR optimisation OR optimize OR optimise OR optimized OR optimised
  OR "process optimization" OR "process optimisation"
  OR "recipe optimization" OR "recipe optimisation"
  OR "parameter optimization" OR "condition optimization" OR "setpoint optimization"
  OR "yield optimization" OR "defect reduction" OR "defect minimization" OR "defect minimisation"
  OR tuning OR "parameter tuning" OR "recipe tuning" OR "auto tuning" OR "auto-tuning"
  OR "self tuning" OR "self-tuning" OR adjustment OR compensation OR "corrective action"
  OR "process recommendation" OR "recipe recommendation" OR "control recommendation"
  OR "recipe generation" OR "condition generation"

  OR autonomous OR autonomic OR "autonomous operation" OR "autonomous control"
  OR "autonomous manufacturing" OR "autonomous fab" OR "autonomous process" OR "autonomous equipment"
  OR "self optimizing" OR "self-optimizing" OR "self optimization" OR "self-optimization"
  OR "self adaptive" OR "self-adaptive" OR "self adjustment" OR "self-adjustment"
  OR "self calibration" OR "self-calibration" OR "self diagnosis" OR "self-diagnosis" OR "self healing" OR "self-healing"
  OR "online learning" OR "on-line learning" OR "continual learning" OR "continuous learning"
  OR "incremental learning" OR "lifelong learning" OR "active learning" OR "semi-supervised learning"
  OR "self-supervised learning" OR "weakly supervised learning" OR "transfer learning" OR "domain adaptation"
  OR "few shot" OR "few-shot" OR "zero shot" OR "zero-shot"
  OR "federated learning" OR "distributed learning"
  OR "model update" OR "model updating" OR "model retraining" OR "model re-training"
  OR "model adaptation" OR "model calibration" OR "model validation"
  OR "model drift" OR "concept drift" OR "data drift" OR "distribution shift"
  OR "model monitoring" OR "model management" OR "model deployment" OR MLOps
  OR "uncertainty estimation" OR "uncertainty quantification"

  OR "digital twin" OR "digital twins" OR "virtual model" OR "virtual fab" OR "virtual factory"
  OR "simulation model" OR "process simulator" OR "fab simulator" OR "equipment simulator"
  OR "hybrid model" OR "physics-informed" OR "physics guided" OR "physics-guided"
  OR "physics based" OR "physics-based" OR "surrogate model"
  OR "decision engine" OR "decision support" OR "decision making"
  OR "recommendation engine" OR "recommendation system"
  OR scheduling OR dispatching OR routing OR "production scheduling" OR "fab scheduling" OR "operation optimization"

  OR "generative AI" OR "generative artificial intelligence" OR "generative model" OR "generative network"
  OR "foundation model" OR "foundation models"
  OR "large language model" OR "large language models" OR LLM OR LLMs
  OR "language model" OR "pretrained model" OR "pre-trained model"
  OR "fine tuning" OR "fine-tuning" OR prompt OR prompts OR prompting OR "prompt engineering"
  OR transformer OR transformers OR "retrieval augmented generation" OR "retrieval-augmented generation" OR RAG
  OR "semantic search" OR "knowledge retrieval" OR "document retrieval"
  OR "AI assistant" OR "manufacturing assistant" OR "fab assistant" OR "process assistant"
  OR "equipment assistant" OR "maintenance assistant" OR copilot OR "co-pilot" OR chatbot
  OR "natural language processing" OR NLP OR "question answering"
  OR "synthetic data" OR "data augmentation" OR "synthetic wafer map" OR "synthetic defect"

  OR "knowledge graph" OR "knowledge base" OR "knowledge representation" OR ontology OR taxonomy
  OR "rule based" OR "rule-based" OR "expert system" OR "inference engine" OR "reasoning engine"
  OR causal OR causality OR "causal model" OR "causal inference" OR "causal graph"
  OR "explainable AI" OR XAI OR explainable OR explanation OR interpretability OR interpretable
  OR "feature importance" OR SHAP OR Shapley OR LIME OR "saliency map" OR "attention map" OR counterfactual

  OR 이상탐지 OR "이상 탐지" OR 이상검출 OR "이상 검출" OR 이상감지 OR "이상 감지"
  OR 비정상탐지 OR "비정상 탐지" OR 이상치탐지 OR "이상치 탐지"
  OR 변화탐지 OR "변화 탐지" OR 드리프트탐지 OR "드리프트 탐지"
  OR 고장검출 OR "고장 검출" OR 고장탐지 OR "고장 탐지" OR 고장분류 OR "고장 분류"
  OR 고장진단 OR "고장 진단" OR 장애진단 OR "장애 진단" OR 오류진단 OR "오류 진단"
  OR 원인분석 OR "원인 분석" OR 근본원인 OR "근본 원인" OR 원인추론 OR "원인 추론"
  OR 결함검출 OR "결함 검출" OR 결함탐지 OR "결함 탐지" OR 결함분류 OR "결함 분류"
  OR 자동결함분류 OR "자동 결함 분류" OR 자동결함리뷰 OR "자동 결함 리뷰"

  OR 가상계측 OR "가상 계측" OR 가상측정 OR "가상 측정" OR 소프트센서 OR "소프트 센서"
  OR 간접측정 OR "간접 측정" OR 추론측정 OR "추론 측정"
  OR 예측 OR 예측모델 OR "예측 모델" OR 추정 OR 추정모델 OR "추정 모델"
  OR 품질예측 OR "품질 예측" OR 공정결과예측 OR "공정 결과 예측"
  OR 수율예측 OR "수율 예측" OR 결함예측 OR "결함 예측" OR 불량예측 OR "불량 예측"
  OR 임계치수예측 OR "임계 치수 예측" OR CD예측 OR "CD 예측"
  OR 오버레이예측 OR "오버레이 예측" OR 막두께예측 OR "막 두께 예측"
  OR 엔드포인트예측 OR "엔드포인트 예측" OR 종점예측 OR "종점 예측"
  OR 잔여수명 OR "잔여 수명" OR 수명예측 OR "수명 예측" OR 유지보수예측 OR "유지 보수 예측"

  OR 공정제어 OR "공정 제어" OR 장비제어 OR "장비 제어" OR 품질제어 OR "품질 제어"
  OR 고급공정제어 OR "고급 공정 제어" OR 런투런제어 OR "런투런 제어"
  OR 피드백제어 OR "피드백 제어" OR 피드포워드제어 OR "피드포워드 제어"
  OR 폐루프제어 OR "폐루프 제어" OR 실시간제어 OR "실시간 제어"
  OR 모델예측제어 OR "모델 예측 제어" OR 예측제어 OR "예측 제어" OR 적응제어 OR "적응 제어"
  OR 최적화 OR 공정최적화 OR "공정 최적화" OR 레시피최적화 OR "레시피 최적화"
  OR 파라미터최적화 OR "파라미터 최적화" OR 조건최적화 OR "조건 최적화"
  OR 수율최적화 OR "수율 최적화" OR 결함저감 OR "결함 저감" OR 불량감소 OR "불량 감소"
  OR 튜닝 OR 파라미터튜닝 OR "파라미터 튜닝" OR 레시피튜닝 OR "레시피 튜닝"
  OR 조건추천 OR "조건 추천" OR 레시피추천 OR "레시피 추천" OR 레시피생성 OR "레시피 생성"

  OR 자율운영 OR "자율 운영" OR 자율제어 OR "자율 제어" OR 자율제조 OR "자율 제조"
  OR 자가학습 OR "자가 학습" OR 자가최적화 OR "자가 최적화" OR 자가적응 OR "자가 적응"
  OR 자가보정 OR "자가 보정" OR 자가진단 OR "자가 진단" OR 자가치유 OR "자가 치유"
  OR 온라인학습 OR "온라인 학습" OR 연속학습 OR "연속 학습" OR 지속학습 OR "지속 학습"
  OR 증분학습 OR "증분 학습" OR 능동학습 OR "능동 학습" OR 반지도학습 OR "반지도 학습"
  OR 자기지도학습 OR "자기 지도 학습" OR 전이학습 OR "전이 학습" OR 도메인적응 OR "도메인 적응"
  OR 연합학습 OR "연합 학습" OR 분산학습 OR "분산 학습"
  OR 모델갱신 OR "모델 갱신" OR 모델업데이트 OR "모델 업데이트"
  OR 모델재학습 OR "모델 재학습" OR 모델재훈련 OR "모델 재훈련"
  OR 모델드리프트 OR "모델 드리프트" OR 개념드리프트 OR "개념 드리프트" OR 데이터드리프트 OR "데이터 드리프트"
  OR 모델관리 OR "모델 관리" OR 모델모니터링 OR "모델 모니터링" OR MLOps

  OR 디지털트윈 OR "디지털 트윈" OR 가상팹 OR "가상 팹" OR 가상공장 OR "가상 공장"
  OR 공정시뮬레이터 OR "공정 시뮬레이터" OR 대리모델 OR "대리 모델" OR 하이브리드모델 OR "하이브리드 모델"
  OR 물리기반 OR "물리 기반" OR 물리정보 OR "물리 정보"
  OR 의사결정 OR "의사 결정" OR 의사결정지원 OR "의사 결정 지원"
  OR 추천엔진 OR "추천 엔진" OR 추천시스템 OR "추천 시스템"
  OR 생산스케줄링 OR "생산 스케줄링" OR 팹스케줄링 OR "팹 스케줄링" OR 운영최적화 OR "운영 최적화"

  OR 생성형AI OR "생성형 AI" OR 생성형인공지능 OR "생성형 인공지능"
  OR 생성모델 OR "생성 모델" OR 기반모델 OR "기반 모델" OR 파운데이션모델 OR "파운데이션 모델"
  OR 대규모언어모델 OR "대규모 언어 모델" OR 대형언어모델 OR "대형 언어 모델" OR 거대언어모델 OR "거대 언어 모델"
  OR 언어모델 OR "언어 모델" OR 프롬프트 OR 프롬프트엔지니어링 OR "프롬프트 엔지니어링"
  OR 검색증강생성 OR "검색 증강 생성" OR 검색기반생성 OR "검색 기반 생성"
  OR AI어시스턴트 OR "AI 어시스턴트" OR 팹어시스턴트 OR "팹 어시스턴트"
  OR 공정어시스턴트 OR "공정 어시스턴트" OR 장비어시스턴트 OR "장비 어시스턴트"
  OR 코파일럿 OR 챗봇 OR 자연어처리 OR "자연어 처리" OR 질의응답 OR "질의 응답"
  OR 합성데이터 OR "합성 데이터" OR 데이터증강 OR "데이터 증강"

  OR 知識グラフ OR ナレッジグラフ OR ルールベース OR エキスパートシステム
  OR 因果推論 OR 説明可能AI OR 説明可能人工知能 OR XAI
  OR 異常検知 OR 異常検出 OR 故障検知 OR 故障診断 OR 欠陥検出 OR 欠陥分類
  OR 仮想計測 OR バーチャルメトロロジ OR ソフトセンサ OR 予測 OR 推定
  OR 工程制御 OR プロセス制御 OR 最適化 OR レシピ最適化 OR 自律制御 OR 自律運用
  OR 生成AI OR 生成型AI OR 基盤モデル OR 大規模言語モデル OR 言語モデル

  OR 知识图谱 OR 知識圖譜 OR 知识库 OR 知識庫 OR 规则模型 OR 規則模型 OR 专家系统 OR 專家系統
  OR 因果推断 OR 因果推論 OR 可解释人工智能 OR 可解釋人工智慧 OR XAI
  OR 异常检测 OR 異常檢測 OR 故障检测 OR 故障檢測 OR 故障诊断 OR 故障診斷
  OR 缺陷检测 OR 缺陷檢測 OR 缺陷分类 OR 缺陷分類
  OR 虚拟量测 OR 虛擬量測 OR 虚拟计量 OR 虛擬計量 OR 软传感器 OR 軟感測器
  OR 预测 OR 預測 OR 估计 OR 估計 OR 工艺控制 OR 製程控制 OR 优化 OR 優化
  OR 配方优化 OR 配方優化 OR 自主控制 OR 自主运行 OR 自主運行
  OR 生成式AI OR 生成式人工智能 OR 生成式人工智慧 OR 基础模型 OR 基礎模型
  OR 大语言模型 OR 大語言模型 OR 语言模型 OR 語言模型
)
```

## 7. AI 알고리즘/기반기술 텍스트 블록

```markdown
(
  regression OR "linear regression" OR "logistic regression" OR "nonlinear regression" OR "non-linear regression"
  OR "ridge regression" OR lasso OR "elastic net" OR "partial least squares" OR PLS
  OR "principal component analysis" OR PCA OR "independent component analysis" OR ICA
  OR "support vector machine" OR SVM OR "support vector regression" OR SVR
  OR "decision tree" OR "decision trees" OR "random forest" OR "random forests"
  OR "gradient boosting" OR "gradient boosted" OR boosting OR AdaBoost OR XGBoost OR LightGBM OR CatBoost
  OR "ensemble learning" OR ensemble OR bagging OR "bootstrap aggregating"
  OR "nearest neighbor" OR "nearest neighbour" OR "k nearest" OR kNN OR KNN
  OR "naive Bayes" OR "naïve Bayes"
  OR "Gaussian process" OR "Gaussian process regression" OR GPR
  OR "Bayesian model" OR "Bayesian network" OR "probabilistic model" OR "probabilistic graphical model"
  OR "Markov model" OR "hidden Markov model" OR HMM OR "Kalman filter" OR "particle filter"
  OR ARIMA OR autoregressive OR "moving average" OR EWMA
  OR clustering OR cluster OR "cluster analysis" OR "k-means" OR "k means" OR DBSCAN
  OR "Gaussian mixture model" OR GMM OR "self organizing map" OR "self-organizing map" OR SOM
  OR "one-class SVM" OR "one class SVM" OR "isolation forest" OR "local outlier factor" OR LOF

  OR "convolutional neural network" OR CNN OR ConvNet OR convolutional
  OR "fully convolutional network" OR FCN OR "residual network" OR ResNet
  OR DenseNet OR EfficientNet OR MobileNet OR YOLO OR "region proposal network" OR RPN
  OR "semantic segmentation" OR "instance segmentation" OR U-Net OR UNet
  OR "encoder decoder" OR "encoder-decoder"
  OR "recurrent neural network" OR RNN OR "long short term memory" OR "long short-term memory" OR LSTM
  OR "gated recurrent unit" OR GRU OR "temporal convolutional network" OR TCN
  OR "sequence model" OR "time-series neural network"
  OR attention OR "attention mechanism" OR "self attention" OR "self-attention"
  OR transformer OR transformers OR "vision transformer" OR ViT OR BERT OR GPT
  OR autoencoder OR "auto-encoder" OR "denoising autoencoder" OR DAE
  OR "variational autoencoder" OR VAE OR "sparse autoencoder"
  OR "generative adversarial network" OR GAN OR "diffusion model" OR "score based model" OR "score-based model"
  OR "graph neural network" OR GNN OR "graph convolutional network" OR GCN
  OR "graph attention network" OR GAT OR "message passing neural network" OR MPNN
  OR "siamese network" OR "triplet network" OR "metric learning" OR "contrastive learning"

  OR "reinforcement learning" OR RL OR "deep reinforcement learning" OR DRL
  OR "Q learning" OR "Q-learning" OR "deep Q network" OR DQN
  OR "actor critic" OR "actor-critic" OR "policy gradient" OR "policy learning"
  OR "proximal policy optimization" OR PPO OR "soft actor critic" OR SAC
  OR "Markov decision process" OR MDP OR "multi armed bandit" OR "multi-armed bandit"
  OR "contextual bandit" OR "reward function" OR reward OR policy OR "control policy"
  OR "Bayesian optimization" OR "Bayesian optimisation"
  OR "black-box optimization" OR "black box optimization"
  OR "gradient-free optimization" OR "derivative-free optimization"
  OR "multi-objective optimization" OR "constrained optimization"
  OR "genetic algorithm" OR "genetic programming" OR "evolutionary algorithm"
  OR "particle swarm optimization" OR PSO OR "ant colony optimization"
  OR "simulated annealing" OR "tabu search" OR "heuristic optimization"
  OR "response surface methodology" OR RSM OR "response surface model"
  OR "design of experiments" OR DOE OR Taguchi

  OR 회귀 OR 회귀분석 OR "회귀 분석" OR 선형회귀 OR "선형 회귀" OR 로지스틱회귀 OR "로지스틱 회귀"
  OR 부분최소제곱 OR "부분 최소 제곱" OR 주성분분석 OR "주성분 분석" OR 독립성분분석 OR "독립 성분 분석"
  OR 서포트벡터머신 OR "서포트 벡터 머신" OR SVM OR 서포트벡터회귀 OR "서포트 벡터 회귀"
  OR 의사결정나무 OR "의사 결정 나무" OR 결정트리 OR "결정 트리"
  OR 랜덤포레스트 OR "랜덤 포레스트" OR 그래디언트부스팅 OR "그래디언트 부스팅"
  OR 앙상블학습 OR "앙상블 학습" OR 배깅 OR 최근접이웃 OR "최근접 이웃"
  OR 나이브베이즈 OR "나이브 베이즈" OR 가우시안프로세스 OR "가우시안 프로세스"
  OR 베이지안모델 OR "베이지안 모델" OR 베이지안네트워크 OR "베이지안 네트워크"
  OR 확률모델 OR "확률 모델" OR 마르코프모델 OR "마르코프 모델" OR 칼만필터 OR "칼만 필터"
  OR 클러스터링 OR 군집화 OR 군집분석 OR "군집 분석" OR k평균 OR "k 평균"
  OR 고립포레스트 OR "고립 포레스트"

  OR 합성곱신경망 OR "합성곱 신경망" OR 컨볼루션신경망 OR "컨볼루션 신경망"
  OR 잔차신경망 OR "잔차 신경망" OR 객체검출망 OR "객체 검출망"
  OR 의미론적분할 OR "의미론적 분할" OR 인스턴스분할 OR "인스턴스 분할"
  OR 순환신경망 OR "순환 신경망" OR 장단기메모리 OR "장단기 메모리"
  OR 어텐션 OR 자기어텐션 OR "자기 어텐션" OR 트랜스포머 OR 비전트랜스포머 OR "비전 트랜스포머"
  OR 오토인코더 OR 오토엔코더 OR 자동부호화기 OR "자동 부호화기"
  OR 변분오토인코더 OR "변분 오토인코더" OR 생성적적대신경망 OR "생성적 적대 신경망"
  OR 확산모델 OR "확산 모델" OR 그래프신경망 OR "그래프 신경망" OR 대조학습 OR "대조 학습"

  OR 강화학습 OR "강화 학습" OR 심층강화학습 OR "심층 강화 학습"
  OR Q러닝 OR "Q 러닝" OR 딥Q네트워크 OR "딥 Q 네트워크"
  OR 액터크리틱 OR "액터 크리틱" OR 정책경사 OR "정책 경사"
  OR 정책최적화 OR "정책 최적화" OR 마르코프결정과정 OR "마르코프 결정 과정"
  OR 밴딧 OR 문맥밴딧 OR "문맥 밴딧" OR 보상함수 OR "보상 함수"
  OR 베이지안최적화 OR "베이지안 최적화" OR 블랙박스최적화 OR "블랙박스 최적화"
  OR 다목적최적화 OR "다목적 최적화" OR 제약최적화 OR "제약 최적화"
  OR 유전알고리즘 OR "유전 알고리즘" OR 진화알고리즘 OR "진화 알고리즘"
  OR 입자군집최적화 OR "입자 군집 최적화" OR 실험계획법 OR "실험 계획법" OR 응답표면 OR "응답 표면"
)
```

## 8. 1차 초광역 복붙용 검색식

아래는 블록명을 그대로 쓴 조립식 버전이다. 실제 검색 시에는 위 블록 내용을 치환한다.

```markdown
(
  SEMICONDUCTOR_CLASS
  OR SEMICONDUCTOR_CORE_TEXT
)
AND
(
  SEMICONDUCTOR_MANUFACTURING_CONTEXT
)
AND
(
  AI_CLASS
  OR AI_CORE_TEXT
  OR AI_FUNCTION_TEXT
  OR AI_ALGORITHM_TEXT
)
```

## 9. 결과가 너무 많을 때의 2차 축소식

1차 검색 결과가 너무 많으면 아래처럼 `AI`가 실제 기능으로 쓰인 문맥을 추가한다.

```markdown
(
  SEMICONDUCTOR_CLASS
  OR SEMICONDUCTOR_CORE_TEXT
)
AND
(
  SEMICONDUCTOR_MANUFACTURING_CONTEXT
)
AND
(
  AI_CORE_TEXT
  OR AI_ALGORITHM_TEXT
)
AND
(
  "anomaly detection" OR "fault detection" OR "defect detection" OR "defect classification"
  OR "virtual metrology" OR "yield prediction" OR "process control" OR "recipe optimization"
  OR "predictive maintenance" OR "digital twin" OR "run-to-run" OR "root cause analysis"
  OR 이상탐지 OR 고장진단 OR 결함검출 OR 결함분류 OR 가상계측 OR 수율예측
  OR 공정제어 OR 레시피최적화 OR 예지보전 OR 디지털트윈 OR 원인분석
)
```

## 10. 선택적 제외 블록

1차에서는 가급적 쓰지 않는다. 검색 결과에 AI 반도체 칩, GPU, NPU, 메모리 컨트롤러, 프로세서 아키텍처 특허가 과도하게 섞일 때만 적용한다.

```markdown
NOT (
  GPU OR NPU OR TPU OR accelerator OR "AI accelerator"
  OR "neural processing unit" OR "tensor processing unit" OR "graphics processing unit"
  OR "AI processor" OR "processor architecture" OR "memory controller"
  OR "large language model accelerator" OR "neural network accelerator"
  OR "in-memory computing" OR "compute-in-memory" OR CIM
  OR "neuromorphic chip" OR "AI chip"
).TI,AB,CL.
```

주의: `CIM`은 `computer integrated manufacturing`과 `compute-in-memory` 양쪽 의미가 있으므로, 제외 블록에서 `CIM` 단독 제외는 위험하다. 결과를 확인한 뒤 필요한 경우에만 쓴다.

## 11. 운용 메모

- 1차 검색은 `TI,AB,CL`만으로 제한하지 말고 가능한 넓은 전문/대표청구항/초록 범위를 우선 사용한다.
- 결과가 너무 많으면 먼저 `AI`, `ML`, `VM`, `IC`, `CD`, `smart`, `automation`, `automated` 같은 짧거나 일반적인 단어를 단독 조건에서 제거한다.
- `fab`은 반도체 팹 의미가 강하지만 일반 fabrication과 섞일 수 있다. 노이즈가 크면 `"semiconductor fab"` 또는 `"wafer fab"` 중심으로 축소한다.
- `substrate`는 디스플레이, 태양전지, PCB까지 넓어진다. 반도체 제조에 집중하려면 `semiconductor OR wafer OR integrated circuit`과 함께 묶는다.
- `digital twin`, `scheduling`, `dispatching`, `MES`는 제조 운영 특허를 잘 잡지만 일반 스마트팩토리 문헌도 많이 들어온다. 결과 검토 후 반도체 공통 블록을 더 강하게 묶는다.
- LLM/생성형 AI는 최근 특허에서 `assistant`, `copilot`, `natural language`, `RAG`, `knowledge retrieval`로 우회 표현되는 경우가 있어 별도 검색을 한 번 더 돌리는 것이 좋다.

## 12. LLM/생성형 AI 별도 보조 검색식

생성형 AI는 일반 AI 검색식에서 묻히기 쉬우므로 별도로 돌린다.

```markdown
(
  "semiconductor manufacturing" OR "wafer fabrication" OR "wafer processing"
  OR "semiconductor process" OR "process recipe" OR "equipment log" OR "process log"
  OR "fault detection" OR FDC OR "process control" OR APC
  OR "virtual metrology" OR "defect inspection" OR "wafer map"
  OR "yield analysis" OR "root cause analysis"
  OR 반도체제조 OR "반도체 제조" OR 웨이퍼공정 OR "웨이퍼 공정"
  OR 반도체공정 OR "반도체 공정" OR 공정레시피 OR "공정 레시피"
  OR 장비로그 OR "장비 로그" OR 공정로그 OR "공정 로그"
  OR 수율분석 OR "수율 분석" OR 결함분석 OR "결함 분석" OR 원인분석 OR "원인 분석"
)
AND
(
  "generative AI" OR "generative artificial intelligence"
  OR "foundation model" OR "large language model" OR "large language models" OR LLM OR LLMs
  OR "language model" OR "pretrained model" OR "pre-trained model"
  OR "fine tuning" OR "fine-tuning" OR prompt OR prompts OR prompting OR "prompt engineering"
  OR "retrieval augmented generation" OR "retrieval-augmented generation" OR RAG
  OR "AI assistant" OR "manufacturing assistant" OR "fab assistant"
  OR "process assistant" OR "equipment assistant" OR "maintenance assistant"
  OR copilot OR "co-pilot" OR chatbot OR "natural language processing" OR NLP
  OR 생성형AI OR "생성형 AI" OR 생성형인공지능 OR "생성형 인공지능"
  OR 기반모델 OR "기반 모델" OR 파운데이션모델 OR "파운데이션 모델"
  OR 대규모언어모델 OR "대규모 언어 모델" OR 대형언어모델 OR "대형 언어 모델"
  OR 거대언어모델 OR "거대 언어 모델" OR 언어모델 OR "언어 모델"
  OR 프롬프트 OR 검색증강생성 OR "검색 증강 생성" OR 코파일럿 OR 챗봇
)
```
