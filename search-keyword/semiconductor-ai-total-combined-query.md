# V5 - A11 반도체 제조 데이터 AI 특허 검색식

이 파일은 A11 과제인 **A.I를 이용한 반도체 장치**에 맞춘 다섯 번째 버전이다.

V2 검색식으로 WIPS ON 상위 200개를 확인한 결과, 제목/출원인 기준 1차 판정에서 **A11 확실 5건 + 후보 13건** 정도만 확인되었다. 나머지는 의료영상, 바이오마커, 차량/모빌리티, 일반 디스플레이 UI, 일반 센서/계측, 배터리, 소프트웨어 AI 문헌이 많았다. 따라서 V3에서는 아래 방향으로 정밀화한다.

1. `display`, `display device`, `display panel`, `substrate`, `AI`, `control`, `diagnosis`, `analysis`, `optimization` 같은 단독 광역어를 줄인다.
2. 반도체/디스플레이/솔라 분야는 **제조, 공정, 장비, 검사, 계측, 결함, 수율 데이터** 문맥이 있어야 통과되게 한다.
3. AI 조건은 단순 `AI`가 아니라 **machine learning, deep learning, neural network, virtual metrology, anomaly/fault/defect detection, prediction, process control, recipe optimization**처럼 기능이 드러나는 표현 중심으로 둔다.
4. 상위 200개에서 확인된 의료, 차량, 일반 UI, 배터리, 일반 소프트웨어 노이즈는 기본 제외식에 반영한다.

중국은 현재 운용처럼 WIPS 국가 필터에서 제외해서 본다.

## V5 변경 요약 (V4 → V5)

V4 이력은 `archive/v4-final-2026-07-07/`에 보관. 설계 프레임·블록별 포함 기준·키워드 채택 원칙은 `semiconductor-ai-query-logic-v5.md` 참조.

1. **일본어/중국어 키워드 전체 삭제** — 현재 운용 검색언어가 "한국어/영어"라서 일/중 원문 텍스트는 매칭 대상이 아님(팀원 실증: 삭제 전후 결과 동일. 일본 특허는 영문 초록으로 매칭됨). 중국/대만 별도 분석 시 전용 검색식에서 부활.
2. **CPC/IPC 확장 (팀원 ms 분석 반영)** — 유효 특허의 약 50%가 H01L 밖에 분류됨(ms 보고서 4-2절). `G01N21/95%`(반도체 시료 검사), `G05B19/418%`(팹 자동화·통합제어) 추가.
3. **A 게이트 반도체 특정어 보강 (ms_v1 대비 갭)** — EUV, photomask, reticle, DRAM, NAND, flash memory, FinFET, foundry, etcher, ion implanter, showerhead, susceptor, electrostatic chuck, EFEM, load port + 한국어(포토마스크, 레티클, 파운드리, 식각기, 증착기, 이온주입기, 정전척). 모두 반도체 한정어라 B·C 게이트와 결합 시 노이즈 위험 낮음.
4. **B 게이트 보강** — EWMA(SPC 기법), OCD/"optical critical dimension"(계측).
5. **C 게이트 AI 기법 보강 (ms_v1 대비 갭)** — LSTM, SVM, k-means, Bayesian, gaussian mixture, hidden markov, prognostics.
6. **기각한 ms_v1 요소(사유)** — 단독 `algorithm`/`model`/`prediction`/`inference`(ms의 lift 수치는 자체 도메인 게이트 내부의 조건부 값. V2에서 단독어 범람 실증), 단독 `clustering`(물리 클러스터 충돌 — ms 보고서도 경고), 단독 `wafer`/`inspection`/`CD`, 단독 `팹`(한 글자 키워드).

## V5 권장 전체 통합 검색식

```markdown
(
  (
    (
      H01L21% OR H01L22% OR H01L21/02% OR H01L21/66% OR H01L21/67% OR H01L21/672%
      OR H01L21/67242 OR H01L21/67276
      OR H01L22/10% OR H01L22/12% OR H01L22/20% OR H01L22/26% OR H01L22/34%
      OR H10B% OR H10D% OR H10F% OR H10N%
      OR G03F1% OR G03F7% OR G03F9%
      OR B24B37%
      OR G01N21/95% OR G05B19/418%
      OR C23C14% OR C23C16% OR C23C18%
      OR H01J37/28% OR H01J37/32%
    ).IPCM,IPC,CPCM,CPC.
    OR
    (
      "semiconductor manufacturing" OR "semiconductor fabrication" OR "semiconductor processing"
      OR "semiconductor process%" OR "semiconductor production"
      OR "semiconductor equipment" OR "semiconductor manufacturing equipment"
      OR "semiconductor processing apparatus" OR "semiconductor processing system"
      OR "semiconductor device manufacturing" OR "semiconductor device fabrication"
      OR "semiconductor manufacturing process%" OR "semiconductor fabrication process%"
      OR "semiconductor manufacturing line" OR "semiconductor fabrication line"
      OR "wafer fab" OR "semiconductor fab" OR foundry OR DRAM OR NAND OR "flash memory" OR FinFET

      OR "wafer manufacturing" OR "wafer fabrication" OR "wafer processing"
      OR "wafer process%" OR "wafer inspection" OR "wafer metrology" OR "wafer test"
      OR "wafer map" OR "wafer defect map" OR "wafer bin map" OR "wafer result%"
      OR "wafer-level inspection" OR "wafer level inspection" OR "wafer-level test" OR "wafer level test"
      OR "wafer sorting" OR "wafer sort" OR "wafer probe"

      OR "substrate processing" OR "semiconductor substrate%" OR "semiconductor substrate processing"
      OR "substrate processing apparatus" OR "substrate processing system"
      OR "substrate inspection" OR "substrate metrology"

      OR "process chamber%" OR "processing chamber%" OR "etch chamber%" OR "deposition chamber%"
      OR "plasma chamber%" OR "reaction chamber%" OR "vacuum chamber%" OR "transfer chamber%"
      OR "load lock" OR "load-lock" OR "processing module%" OR "process module%"
      OR etcher OR "ion implanter" OR showerhead OR susceptor OR "electrostatic chuck" OR EFEM OR "load port"

      OR "plasma processing" OR "plasma process%" OR "plasma treatment"
      OR "etch process%" OR "etching process%" OR "plasma etching" OR "dry etching" OR "wet etching"
      OR "reactive ion etching" OR RIE OR "atomic layer etching" OR ALE
      OR "deposition process%" OR "thin film deposition" OR CVD OR "chemical vapor deposition"
      OR PECVD OR LPCVD OR MOCVD OR ALD OR "atomic layer deposition"
      OR PVD OR sputtering OR epitaxy OR epitaxial OR "seed layer"
      OR lithography OR photolithography OR "exposure apparatus"
      OR "overlay metrology" OR "wafer alignment" OR "mask alignment" OR "alignment mark"
      OR "critical dimension" OR "CD-SEM" OR CDSEM
      OR CMP OR "chemical mechanical polishing" OR "chemical mechanical planarization"
      OR "wafer polishing" OR planarization OR "wafer cleaning" OR "wet cleaning"
      OR "annealing process" OR "thermal annealing" OR "rapid thermal annealing" OR "laser annealing"
      OR "thermal oxidation" OR "oxidation process" OR "diffusion process" OR "thermal diffusion"
      OR "dopant diffusion" OR "diffusion furnace" OR "ion implantation"
      OR "patterning process" OR "pattern inspection" OR "mask inspection" OR "EUV lithography"
      OR EUV OR photomask OR reticle

      OR 반도체제조 OR "반도체 제조" OR 반도체공정 OR "반도체 공정"
      OR 반도체장비 OR "반도체 장비" OR 반도체소자제조 OR "반도체 소자 제조"
      OR 웨이퍼제조 OR "웨이퍼 제조" OR 웨이퍼공정 OR "웨이퍼 공정"
      OR 웨이퍼처리 OR "웨이퍼 처리" OR 웨이퍼검사 OR "웨이퍼 검사"
      OR 웨이퍼계측 OR "웨이퍼 계측" OR 웨이퍼맵 OR "웨이퍼 맵" OR 빈맵 OR "빈 맵"
      OR 기판처리 OR "기판 처리" OR 기판공정 OR "기판 공정" OR 기판검사 OR "기판 검사"
      OR 공정챔버 OR "공정 챔버" OR 처리챔버 OR "처리 챔버"
      OR 플라즈마공정 OR "플라즈마 공정" OR 식각공정 OR "식각 공정"
      OR 증착공정 OR "증착 공정" OR 박막증착 OR "박막 증착"
      OR 노광공정 OR "노광 공정" OR 리소그래피 OR 포토리소그래피
      OR 오버레이계측 OR "오버레이 계측" OR 임계치수 OR 선폭
      OR 패터닝 OR 마스크검사 OR "마스크 검사"
      OR 화학기계연마 OR 연마공정 OR "연마 공정" OR 평탄화공정 OR "평탄화 공정"
      OR 세정공정 OR "세정 공정" OR 열처리공정 OR "열처리 공정" OR 이온주입
      OR 포토마스크 OR 레티클 OR 파운드리 OR 식각기 OR 증착기 OR 이온주입기 OR 정전척
    ).TI,AB,CL.
    OR
    (
      (
        H10K% OR G02F1% OR H01L31% OR H01L27%
      ).IPCM,IPC,CPCM,CPC.
      AND
      (
        "display manufacturing" OR "display fabrication" OR "display panel manufacturing"
        OR "display panel fabrication" OR "panel manufacturing" OR "panel fabrication"
        OR "OLED manufacturing" OR "OLED fabrication" OR "OLED deposition"
        OR "TFT array process" OR "TFT array manufacturing"
        OR "glass substrate processing" OR "glass substrate inspection" OR "panel inspection" OR "panel metrology"
        OR "display defect inspection" OR "display process data" OR "panel process data"
        OR "solar cell manufacturing" OR "solar cell fabrication" OR "solar cell process%"
        OR "photovoltaic manufacturing" OR "photovoltaic fabrication" OR "photovoltaic process%"
        OR "PV cell manufacturing" OR "PV cell fabrication"
        OR "solar cell inspection" OR "photovoltaic inspection" OR "solar cell metrology"
        OR 디스플레이제조 OR "디스플레이 제조" OR 디스플레이공정 OR "디스플레이 공정"
        OR 표시장치제조 OR "표시장치 제조" OR 패널제조 OR "패널 제조" OR 패널공정 OR "패널 공정"
        OR 글라스기판처리 OR "글라스 기판 처리" OR 유리기판처리 OR "유리 기판 처리"
        OR 패널검사 OR "패널 검사" OR 패널계측 OR "패널 계측"
        OR 태양전지제조 OR "태양 전지 제조" OR 태양전지공정 OR "태양 전지 공정"
        OR 태양전지검사 OR "태양 전지 검사" OR 광전지제조 OR "광전지 제조"
      ).TI,AB,CL.
    )
  )
  AND
  (
    "equipment data" OR "tool data" OR "chamber data" OR "machine data"
    OR "equipment log%" OR "tool log%" OR "process log%" OR "event log%"
    OR "sensor data" OR "sensor signal%" OR "process signal%" OR "in-situ signal%" OR "in situ signal%"
    OR "trace data" OR "process trace" OR "process trace data" OR "sensor trace" OR "equipment trace" OR "tool trace"
    OR "time series data" OR "time-series data" OR "temporal data" OR telemetry
    OR "status data" OR "state data" OR "operating data" OR "operation data"
    OR "tool state" OR "equipment state" OR "machine state" OR "chamber state"
    OR "measurement data" OR "metrology data" OR "inspection data"
    OR "chamber pressure" OR "chamber temperature" OR "wafer temperature"
    OR "RF power" OR "RF signal" OR "RF reflection" OR "plasma parameter%" OR "plasma impedance"
    OR "optical emission" OR OES OR "emission spectrum" OR "plasma spectrum" OR "plasma spectra"
    OR "mass flow" OR "gas flow" OR "flow rate" OR MFC
    OR "vacuum pressure" OR "chamber vibration" OR "motor current" OR "valve position"
    OR "throttle valve" OR "pump speed" OR endpoint OR "end point" OR "end-point" OR "endpoint signal"
    OR "equipment data acquisition" OR "SEMI EDA" OR "SECS/GEM" OR SECS OR GEM300 OR "GEM 300"
    OR SVID OR CEID OR "status variable" OR "collection event" OR "data collection plan" OR DCP

    OR "process data" OR "manufacturing data" OR "fabrication data" OR "production data"
    OR "process history" OR "manufacturing history" OR "wafer history" OR "lot history"
    OR "run data" OR "run history" OR "process record%"
    OR recipe OR recipes OR "process recipe%" OR "manufacturing recipe%" OR "tool recipe%" OR "equipment recipe%"
    OR "recipe parameter%" OR "recipe setting%" OR "recipe data"
    OR "process condition%" OR "processing condition%" OR "process parameter%" OR "control parameter%"
    OR "operating parameter%" OR setpoint OR "set point" OR "target value%" OR "process variable%"
    OR "process window" OR "process margin" OR "process variation" OR "process drift" OR "process excursion"
    OR APC OR "advanced process control" OR SPC OR "statistical process control" OR EWMA
    OR FDC OR "fault detection and classification"
    OR R2R OR "run-to-run" OR "run to run" OR "feedforward control" OR "feedback control" OR "closed loop" OR "closed-loop"

    OR "inspection result%" OR "metrology result%" OR "measurement result%" OR "test result%"
    OR "process result%" OR "processing result%" OR "manufacturing result%"
    OR "wafer result%" OR "substrate result%" OR "panel result%" OR "glass result%"
    OR "wafer inspection" OR "substrate inspection" OR "panel inspection" OR "glass inspection"
    OR "defect inspection" OR "optical inspection" OR "e-beam inspection" OR "electron beam inspection"
    OR "SEM inspection" OR "defect review" OR ADR OR "automatic defect review"
    OR "wafer metrology" OR "process metrology" OR "inline metrology" OR "in-line metrology"
    OR "in situ metrology" OR "in-situ metrology" OR "optical metrology" OR scatterometry OR ellipsometry
    OR OCD OR "optical critical dimension"
    OR reflectometry OR interferometry OR spectroscopy
    OR "CD-SEM" OR CDSEM OR "critical dimension SEM" OR "overlay metrology" OR "film metrology"
    OR "overlay correction" OR "overlay control"
    OR "thickness measurement" OR "profile measurement" OR "electrical measurement"
    OR "parametric test" OR "parametric data" OR E-test OR "electrical test"
    OR "wafer sort" OR "wafer test" OR WAT OR "wafer acceptance test" OR "process control monitor"
    OR "wafer probe" OR "probe test" OR "wafer-level test" OR "wafer level test"
    OR "defect data" OR "defect map" OR "wafer defect map" OR "defect image"
    OR "defect pattern" OR "defect signature" OR "defect classification" OR "defect detection"
    OR "killer defect" OR "nuisance defect" OR "systematic defect" OR "random defect" OR "pattern defect"
    OR "particle defect" OR "contamination defect" OR "residue defect" OR "scratch defect"
    OR "line collapse" OR "pattern collapse" OR "lithography hotspot" OR "pattern hotspot"
    OR "EUV stochastic%" OR "stochastic defect%" OR "line break" OR "missing contact" OR "merged contact"
    OR "inspection image" OR "wafer image" OR "SEM image" OR "optical image"
    OR "wafer map" OR "bin map" OR "wafer bin map" OR WBM OR "failure map" OR "yield map" OR "spatial map"
    OR "yield data" OR "yield loss" OR "yield analysis" OR "yield management" OR "yield excursion"
    OR "critical dimension" OR "CD variation" OR "CD uniformity" OR linewidth OR "line width"
    OR LER OR LWR OR EPE OR "edge placement error" OR "overlay error"
    OR "film thickness" OR "thickness uniformity" OR nonuniformity OR "etch depth" OR "etch rate" OR "removal rate"

    OR 장비데이터 OR "장비 데이터" OR 툴데이터 OR "툴 데이터" OR 챔버데이터 OR "챔버 데이터"
    OR 장비로그 OR "장비 로그" OR 공정로그 OR "공정 로그" OR 이벤트로그 OR "이벤트 로그"
    OR 센서데이터 OR "센서 데이터" OR 센서신호 OR "센서 신호" OR 공정신호 OR "공정 신호"
    OR 트레이스데이터 OR "트레이스 데이터" OR 시계열데이터 OR "시계열 데이터"
    OR 상태데이터 OR "상태 데이터" OR 운전데이터 OR "운전 데이터"
    OR 챔버압력 OR "챔버 압력" OR 챔버온도 OR "챔버 온도" OR 웨이퍼온도 OR "웨이퍼 온도"
    OR RF전력 OR "RF 전력" OR 플라즈마파라미터 OR "플라즈마 파라미터" OR 광방출 OR 발광스펙트럼
    OR 질량유량 OR 가스유량 OR 유량데이터 OR "유량 데이터" OR 진공압력 OR "진공 압력"
    OR 엔드포인트신호 OR "엔드포인트 신호" OR 종점신호 OR "종점 신호"

    OR 공정데이터 OR "공정 데이터" OR 제조데이터 OR "제조 데이터" OR 생산데이터 OR "생산 데이터"
    OR 공정이력 OR "공정 이력" OR 제조이력 OR "제조 이력" OR 웨이퍼이력 OR "웨이퍼 이력" OR 로트이력 OR "로트 이력"
    OR 런데이터 OR "런 데이터" OR 런이력 OR "런 이력" OR 공정기록 OR "공정 기록"
    OR 레시피 OR 공정레시피 OR "공정 레시피" OR 레시피파라미터 OR "레시피 파라미터"
    OR 공정조건 OR "공정 조건" OR 공정파라미터 OR "공정 파라미터" OR 제어파라미터 OR "제어 파라미터"
    OR 설정값 OR 목표값 OR 공정변수 OR "공정 변수" OR 공정편차 OR 공정드리프트 OR 공정일탈
    OR 고급공정제어 OR 통계공정제어 OR 고장검출분류 OR 런투런 OR "런 투 런" OR "런-투-런"

    OR 검사결과 OR "검사 결과" OR 계측결과 OR "계측 결과" OR 측정결과 OR "측정 결과" OR 시험결과 OR "시험 결과"
    OR 공정결과 OR "공정 결과" OR 제조결과 OR "제조 결과" OR 웨이퍼결과 OR "웨이퍼 결과" OR 기판결과 OR "기판 결과"
    OR 패널결과 OR "패널 결과" OR 글라스결과 OR "글라스 결과"
    OR 웨이퍼검사 OR "웨이퍼 검사" OR 기판검사 OR "기판 검사" OR 패널검사 OR "패널 검사"
    OR 결함검사 OR "결함 검사" OR 광학검사 OR 전자빔검사 OR SEM검사 OR 결함리뷰 OR 자동결함리뷰
    OR 웨이퍼계측 OR "웨이퍼 계측" OR 공정계측 OR "공정 계측" OR 인라인계측 OR "인라인 계측"
    OR 결함데이터 OR "결함 데이터" OR 결함맵 OR "결함 맵" OR 웨이퍼맵 OR "웨이퍼 맵" OR 빈맵 OR "빈 맵"
    OR 결함이미지 OR "결함 이미지" OR 결함패턴 OR "결함 패턴" OR 결함시그니처 OR "결함 시그니처"
    OR 결함분류 OR "결함 분류" OR 결함검출 OR "결함 검출" OR 결함탐지 OR "결함 탐지"
    OR 수율데이터 OR "수율 데이터" OR 수율손실 OR "수율 손실" OR 수율분석 OR "수율 분석" OR 수율관리 OR "수율 관리"
    OR 임계치수 OR 선폭 OR 오버레이오차 OR "오버레이 오차" OR 막두께 OR "막 두께" OR 두께균일도 OR "두께 균일도"
    OR 식각깊이 OR "식각 깊이" OR 식각률 OR 제거율
  ).TI,AB,CL.
  AND
  (
    (
      G06N% OR G06F18% OR G06V10% OR G06V20% OR G06V30% OR G06T7%
    ).IPCM,IPC,CPCM,CPC.
    OR
    (
      "artificial intelligence" OR "artificial-intelligence" OR "AI-based" OR "AI based"
      OR "AI-assisted" OR "AI assisted" OR "A.I." OR "A.I"
      OR "machine learning" OR "machine-learning" OR "ML-based" OR "ML based"
      OR "deep learning" OR "deep-learning" OR "DL-based" OR "DL based"
      OR "neural network%" OR "artificial neural network%" OR "deep neural network%" OR DNN OR CNN OR RNN
      OR "convolutional neural" OR "recurrent neural" OR "graph neural network%"
      OR "transformer model%" OR "transformer network%" OR "vision transformer"
      OR "reinforcement learning" OR "support vector" OR "random forest" OR "gradient boosting"
      OR "decision tree" OR autoencoder OR "auto-encoder" OR "generative adversarial" OR "generative model%"
      OR LSTM OR SVM OR "k-means" OR Bayesian OR "gaussian mixture" OR "hidden markov" OR prognostics
      OR "large language model%" OR "foundation model%"
      OR "learning model%" OR "trained model%" OR "training model%"
      OR "prediction model%" OR "predictive model%" OR "classification model%" OR "regression model%"
      OR "estimation model%" OR "diagnosis model%" OR "diagnostic model%" OR "control model%"
      OR "data driven model%" OR "data-driven model%" OR "data based model%" OR "data-based model%"
      OR "model training" OR "training data" OR "learning data" OR "feature extraction" OR "feature learning"
      OR "pattern recognition" OR "representation learning"

      OR "anomaly detection" OR "abnormal detection" OR "abnormality detection"
      OR "outlier detection" OR "novelty detection" OR "deviation detection" OR "change detection" OR "drift detection"
      OR "fault detection" OR "fault classification" OR "fault diagnosis" OR "fault isolation"
      OR "failure detection" OR "failure diagnosis" OR "failure prediction"
      OR "root cause analysis" OR "cause analysis" OR "cause identification"
      OR "defect detection" OR "defect classification" OR "defect recognition" OR "defect identification"
      OR "automatic defect classification" OR ADR OR "automatic defect review"

      OR "virtual metrology" OR "virtual measurement" OR "soft sensor" OR "soft sensing"
      OR "inferential sensor" OR "inferential measurement" OR "proxy metrology"
      OR "quality prediction" OR "quality estimation" OR "process result prediction" OR "process outcome prediction"
      OR "yield prediction" OR "yield estimation" OR "defect prediction" OR "defect probability"
      OR "critical dimension prediction" OR "CD prediction" OR "overlay prediction" OR "film thickness prediction"
      OR "endpoint prediction" OR "remaining useful life" OR RUL

      OR "process control" OR "equipment control" OR "tool control" OR "chamber control" OR "fab control"
      OR "advanced process control" OR APC OR "run-to-run control" OR R2R
      OR "feedback control" OR "feedforward control" OR "closed-loop control" OR "real-time control"
      OR "model predictive control" OR MPC OR "predictive control" OR "adaptive control"
      OR "process optimization" OR "process optimisation" OR "recipe optimization" OR "recipe optimisation"
      OR "parameter optimization" OR "condition optimization" OR "yield optimization"
      OR "recipe tuning" OR "parameter tuning" OR "auto tuning" OR "self tuning"
      OR "corrective action" OR "process recommendation" OR "recipe recommendation" OR "control recommendation"
      OR "recipe generation" OR "condition generation"
      OR "chamber matching" OR "tool matching" OR "equipment matching"
      OR "predictive maintenance" OR "condition based maintenance" OR "condition-based maintenance"
      OR "digital twin" OR "virtual fab" OR "virtual manufacturing" OR "surrogate model"
      OR "physics-informed" OR "physics based" OR "physics-based"

      OR 인공지능 OR "인공 지능" OR AI기반 OR "AI 기반" OR AI이용 OR "AI 이용" OR "AI를 이용"
      OR 에이아이기반 OR "에이아이 기반" OR 기계학습 OR "기계 학습" OR 머신러닝 OR "머신 러닝"
      OR 딥러닝 OR "딥 러닝" OR 심층학습 OR "심층 학습"
      OR 신경망 OR 뉴럴네트워크 OR "뉴럴 네트워크" OR 인공신경망 OR "인공 신경망"
      OR 강화학습 OR "강화 학습" OR 오토인코더 OR 생성모델 OR "생성 모델"
      OR 학습모델 OR "학습 모델" OR 훈련모델 OR "훈련 모델" OR 예측모델 OR "예측 모델"
      OR 분류모델 OR "분류 모델" OR 회귀모델 OR "회귀 모델" OR 추정모델 OR "추정 모델" OR 진단모델 OR "진단 모델"
      OR 데이터기반모델 OR "데이터 기반 모델" OR 데이터구동모델 OR "데이터 구동 모델"
      OR 특징추출 OR "특징 추출" OR 특징학습 OR "특징 학습" OR 패턴인식 OR "패턴 인식"

      OR 이상탐지 OR "이상 탐지" OR 이상검출 OR "이상 검출" OR 이상감지 OR "이상 감지"
      OR 비정상탐지 OR "비정상 탐지" OR 이상치탐지 OR "이상치 탐지" OR 드리프트탐지 OR "드리프트 탐지"
      OR 고장검출 OR "고장 검출" OR 고장탐지 OR "고장 탐지" OR 고장분류 OR "고장 분류" OR 고장진단 OR "고장 진단"
      OR 결함검출 OR "결함 검출" OR 결함탐지 OR "결함 탐지" OR 결함분류 OR "결함 분류" OR 자동결함분류 OR "자동 결함 분류"
      OR 원인분석 OR "원인 분석" OR 근본원인 OR "근본 원인" OR 인과분석 OR "인과 분석"
      OR 가상계측 OR "가상 계측" OR 가상측정 OR "가상 측정" OR 소프트센서 OR "소프트 센서"
      OR 품질예측 OR "품질 예측" OR 공정결과예측 OR "공정 결과 예측"
      OR 수율예측 OR "수율 예측" OR 결함예측 OR "결함 예측" OR 임계치수예측 OR "임계 치수 예측"
      OR 오버레이예측 OR "오버레이 예측" OR 막두께예측 OR "막 두께 예측" OR 엔드포인트예측 OR "엔드포인트 예측"
      OR 공정제어 OR "공정 제어" OR 장비제어 OR "장비 제어" OR 고급공정제어 OR "고급 공정 제어"
      OR 런투런제어 OR "런투런 제어" OR 피드백제어 OR "피드백 제어" OR 폐루프제어 OR "폐루프 제어"
      OR 모델예측제어 OR "모델 예측 제어" OR 예측제어 OR "예측 제어" OR 적응제어 OR "적응 제어"
      OR 공정최적화 OR "공정 최적화" OR 레시피최적화 OR "레시피 최적화"
      OR 파라미터최적화 OR "파라미터 최적화" OR 조건최적화 OR "조건 최적화" OR 수율최적화 OR "수율 최적화"
      OR 레시피추천 OR "레시피 추천" OR 공정추천 OR "공정 추천" OR 조건추천 OR "조건 추천" OR 레시피생성 OR "레시피 생성"
      OR 예지보전 OR 예방보전 OR 예측정비 OR 잔여수명 OR 잔존수명
      OR 디지털트윈 OR "디지털 트윈" OR 가상팹 OR "가상 팹" OR 가상제조 OR "가상 제조"
    ).TI,AB,CL.
  )
)
NOT
(
  medical OR patient OR clinical OR disease OR tumor OR cancer OR dementia
  OR MRI OR "magnetic resonance imaging" OR ultrasound OR "ultrasonic diagnosis" OR "ultrasonic imaging"
  OR endoscope OR endoscopic OR catheter OR surgical OR surgery
  OR retina OR retinal OR fundus OR cardiac OR nasal
  OR "brain imaging" OR "brain tumor" OR "brain activity" OR "brain wave"
  OR biomarker OR biomarkers OR "blood sample" OR "blood glucose" OR "blood pressure" OR serum OR "body temperature"
  OR "medical image" OR "medical imaging" OR "diagnostic device" OR "in vitro diagnostic"

  OR "vehicle display" OR "in-vehicle" OR "vehicle-mounted" OR "autonomous driving" OR "autonomous vehicle"
  OR "driver assistance" OR "advanced driver" OR "self-driving" OR "vehicle control" OR "vehicle navigation"
  OR "automotive part%" OR "automobile part%"
  OR aircraft OR "aerial vehicle" OR drone
  OR "head-up display" OR HUD OR "head mounted display" OR "head-mounted display"
  OR "gaze tracking" OR "eye tracking" OR "augmented reality" OR "virtual reality"
  OR "video game" OR "game console" OR gameplay OR "video highlight" OR "social distancing"
  OR "graphical user interface layout" OR "image forming apparatus"

  OR "battery cell" OR "rechargeable battery" OR "secondary battery" OR "battery pack" OR "battery module"
  OR "negative electrode" OR "positive electrode" OR "battery separator"
  OR "fuel cell" OR "solar power generation system"

  OR qubit OR "quantum computing" OR "quantum bit" OR "quantum processor" OR "quantum device" OR "quantum information" OR superconducting OR memristor

  OR agriculture OR agricultural OR "seed germination" OR "plant growth" OR soil
  OR fermentation OR enzyme OR fragrance OR laundry OR cooking
  OR "water quality" OR "water treatment" OR "drinking water" OR "waste water" OR wastewater
  OR triglyceride OR rockburst OR geology OR "coal mine" OR "coal mining" OR oilfield OR wellhead
  OR "wind turbine" OR tire OR tyre
  OR "building construction" OR "civil engineering" OR "construction site" OR "power plant" OR "chemical plant"
  OR "financial time series" OR "financial data"
  OR insurance OR banking OR shopping OR "conditional sales" OR "project management"
  OR cybersecurity OR "network vulnerability" OR "security vulnerability" OR microservices OR "data transparency platform"

  OR 의료 OR 환자 OR 질병 OR 종양 OR 암 OR 치매 OR 바이오마커 OR 혈액 OR 혈청
  OR 의료영상 OR "의료 영상" OR "초음파 진단" OR "초음파 영상" OR 내시경 OR 망막 OR 수술
  OR 자율주행 OR "운전자 보조" OR 차량제어 OR "차량 제어" OR "차량용 디스플레이" OR "차량 디스플레이"
  OR 자동차부품 OR "자동차 부품"
  OR 항공기 OR 드론 OR 게임 OR 증강현실 OR 가상현실 OR 시선추적 OR "시선 추적"
  OR 이차전지 OR 배터리 OR 음극 OR 분리막 OR 연료전지 OR 태양광발전 OR "태양광 발전"
  OR 큐비트 OR 양자컴퓨팅 OR "양자 컴퓨팅" OR 양자소자 OR "양자 소자" OR 양자장치 OR "양자 장치" OR 초전도 OR 멤리스터
  OR 농업 OR 종자 OR 토양 OR 발효 OR 효소 OR 조리흄 OR 반려동물 OR 수질 OR 암반
  OR 보험 OR 은행 OR 쇼핑 OR 보안취약점
).TI,AB,CL.
```

## V5에서 의도적으로 뺀 표현

- `display`, `display device`, `display panel` 단독어
- `substrate%`, `기판` 단독어
- `AI`, `ML`, `control`, `prediction`, `estimate`, `diagnosis`, `analysis`, `optimization`, `model` 단독어
- `inspection`, `metrology`, `image`, `sensor`, `temperature`, `pressure`, `defect`, `yield`, `data` 단독어

이 단독어들은 A11 핵심 문헌에서도 자주 나오지만, WIPS 실제 결과에서는 의료, 차량, 일반 UI, 일반 센서, 일반 제조 특허를 훨씬 더 많이 끌어왔다. V5에서는 복합 표현으로만 남겼다.

## V5 검색 후 확인할 기준

상위 200개에서 아래 비율이면 성능이 괜찮다고 본다.

- A11 확실 + 후보가 40건 이상: 실사용 가능
- A11 확실 + 후보가 25~39건: 아직 넓지만 분석 가능
- A11 확실 + 후보가 25건 미만: `display`, `substrate`, `AI/control` 계열 노이즈가 아직 남은 것

V5가 너무 많이 줄어들면 아래 표현을 일부 복원한다.

```markdown
OR "semiconductor wafer%" OR "silicon wafer%" OR "processed wafer%"
OR "target substrate%" OR "processed substrate%"
OR "display process%" OR "display inspection" OR "display metrology"
OR "solar cell result%" OR "photovoltaic result%"
OR "data-driven" OR "data based" OR "predictive"
OR 반도체웨이퍼 OR "반도체 웨이퍼" OR 처리기판 OR "처리 기판"
OR 디스플레이검사 OR "디스플레이 검사" OR 태양전지결과 OR "태양 전지 결과"
```
