**Volume 25. Testing Validation and Benchmarking**


# Chapter 05. Field Testing Methodology

##  

## 05.01. Field Test Planning Scope Protocol Safety Plan

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

Field testing converts laboratory confidence into evidence that a robotic system can operate safely and predictably under real environmental conditions. A field test plan should define why the campaign is being conducted, which system capabilities are being evaluated, what operational conditions are permitted, and what evidence must be collected. The planning process establishes a controlled bridge between simulation, HIL, integration testing, and deployment-oriented validation. Volume_25_Testing_Validation_an...

The scope should identify the robot configuration, software and firmware versions, sensor suite, compute platform, payload, communication infrastructure, test environment, operators, and supporting equipment. It should also state which functions are inside or outside the campaign boundary. Navigation, manipulation, locomotion, perception, communication, autonomy, safety functions, and human interaction may require different test conditions and acceptance criteria.

A useful scope separates nominal operation from degraded and abnormal operation. Nominal tests demonstrate expected behavior within the intended operational design domain, while degraded tests introduce controlled limitations such as reduced visibility, communication loss, localization uncertainty, sensor degradation, low battery state, or restricted maneuvering space. Abnormal conditions should only be exercised when appropriate containment and recovery mechanisms are available.

Every field campaign should be driven by explicit objectives that can be traced to system requirements, identified hazards, previous verification results, or unresolved engineering risks. Statements such as "test navigation performance" are too broad. A stronger objective specifies the capability, operating condition, measurable result, and acceptance boundary, allowing each test execution to produce evidence that can later support validation, regression analysis, or certification activities.

The test protocol translates these objectives into repeatable operational procedures. Each test case should describe initial conditions, environment configuration, robot state, required personnel, instrumentation, execution sequence, expected behavior, termination conditions, and data to be recorded. The protocol should minimize uncontrolled variation while preserving the environmental realism that distinguishes field testing from simulation and laboratory verification.

Configuration control is essential because field results are meaningful only when the tested system can be reconstructed. The test record should therefore capture software commit or release identifiers, AI model versions, calibration files, parameter sets, firmware revisions, maps, mission definitions, hardware configuration, and relevant infrastructure settings. Any modification during the campaign should be logged and assessed before results from different configurations are combined.

The environment itself must be treated as part of the test configuration. Terrain geometry, floor condition, slope, illumination, weather, temperature, obstacles, pedestrian activity, electromagnetic conditions, GNSS availability, network coverage, and operational traffic can influence robot behavior. Relevant environmental variables should therefore be measured or documented so that failures can be distinguished from uncontrolled changes in test conditions.

A field safety plan begins with hazard identification before robot motion is authorized. Potential hazards include collision, crushing, trapping, falling, uncontrolled acceleration, actuator malfunction, battery incidents, dropped payloads, loss of communication, unstable locomotion, unexpected AI decisions, and interaction with people or vehicles. The plan should connect each credible hazard to preventive controls, monitoring requirements, intervention mechanisms, and emergency responses.

Risk controls should follow a layered philosophy rather than depending on operator reaction alone. Physical barriers, exclusion zones, speed and force limits, geofencing, safety-rated functions, emergency stops, remote disable mechanisms, protective equipment, spotters, and procedural controls may be combined according to the platform and environment. Higher-risk tests should begin with conservative limits and expand only after predefined readiness conditions have been demonstrated.

Roles and authority must be established before execution. A test director normally controls the campaign, while operators command the robot and safety personnel monitor hazards independently of performance objectives. Instrumentation engineers, observers, maintenance personnel, and data engineers may support execution. Most importantly, personnel must know who has unconditional authority to stop a test when an unsafe, unexpected, or insufficiently understood condition occurs.

A pre-test readiness review should confirm that prerequisite verification has been completed and that the field configuration is suitable for operation. This includes checking mechanical integrity, battery condition, sensor calibration, actuator health, localization readiness, network connectivity, logging capacity, safety devices, emergency-stop operation, test-zone control, weather constraints, personnel communications, and recovery equipment. Failed readiness items should prevent execution until formally resolved.

Go/no-go criteria provide an objective boundary between preparation and execution. A test should not begin merely because personnel and equipment are available. Required safety functions must be operational, environmental conditions must remain inside authorized limits, the intended software and model configuration must be verified, data acquisition must be functioning, and emergency response resources must be ready. The test director should record the authorization decision.

Execution should follow the approved protocol while allowing controlled responses to real-world uncertainty. Operators should not silently improvise around unexpected behavior because such changes can invalidate evidence or introduce new hazards. Deviations should be recorded with their time, reason, authorization, and impact on the test. Significant deviations should trigger termination, reconfiguration, or creation of a revised test case rather than informal continuation.

Clear abort criteria are especially important for autonomous and AI-enabled robots. Examples include unexpected entry into an exclusion zone, excessive tracking error, unstable motion, repeated perception failure, abnormal actuator temperature, loss of localization, communication timeout, safety-monitor faults, unexpected human proximity, or behavior outside the validated envelope. Abort thresholds should be defined before testing so that safety decisions are not delayed by performance pressure.

Emergency procedures must address what happens after an abort command as well as how the command is issued. The plan should define methods for controlled stopping, emergency stopping, power isolation, securing unstable hardware, recovering disabled robots, handling battery or fire events, notifying responsible personnel, and preserving evidence. Personnel should rehearse critical responses before high-energy, high-speed, aerial, or human-proximate tests are attempted.

Field testing also requires disciplined data planning. The campaign should identify which telemetry, sensor streams, control commands, system states, safety events, operator actions, timestamps, environmental measurements, and external observations are necessary to evaluate each objective. Synchronization between data sources is critical because many field failures can only be reconstructed by correlating perception, planning, control, hardware, network, and human events.

Pass/fail criteria should be defined before examining final results. Criteria may combine quantitative thresholds, behavioral requirements, safety constraints, and completion conditions. A robot may complete a mission yet fail because it violated a minimum separation distance, exceeded a control limit, required unauthorized intervention, or generated an unsafe recovery behavior. Conversely, a controlled safety stop may represent correct system behavior rather than a failed test.

Repeated trials are necessary when performance is affected by stochastic AI behavior, perception uncertainty, environmental variability, or human interaction. The protocol should define sufficient repetition and variation to characterize consistency rather than selecting a single successful demonstration. Conditions and outcomes should be recorded for unsuccessful trials with the same rigor as successful ones, since failure distributions frequently reveal limitations that average performance metrics conceal.

Field campaigns should progress incrementally from low-risk controlled conditions toward increasingly representative operation. A mobile robot might advance from an isolated test area to structured obstacles and then mixed traffic; a legged robot from level terrain to irregular surfaces; a humanoid from constrained tasks to human interaction; and a UAV from restricted flight envelopes to representative missions. The chapter structure explicitly extends field methodology across these platform classes. Volume_25_Testing_Validation_an...

Completion of a field test does not automatically constitute acceptance. After execution, engineers should verify data integrity, classify anomalies, compare measurements against acceptance criteria, identify protocol deviations, and determine whether additional trials are necessary. Safety events and unexpected behaviors should be preserved for incident investigation and root-cause analysis rather than excluded from the dataset simply because they invalidate an individual run.

A well-designed field test plan ultimately creates traceability from requirement and risk to protocol, configuration, execution record, measured evidence, and engineering decision. This discipline makes field testing more than a demonstration of robot capability. It becomes a reproducible validation process that supports subsequent KPI analysis, incident investigation, regression testing, certification evidence collection, and defensible decisions about whether the system is ready for broader deployment. Volume_25_Testing_Validation_an...

현장 시험(Field Testing)은 실험실에서 확보한 신뢰성을 실제 환경 조건에서 로봇 시스템이 안전하고 예측 가능하게 작동할 수 있다는 증거로 전환하는 과정이다. 현장 시험 계획(Field Test Plan)은 시험 캠페인(Test Campaign)을 수행하는 목적, 평가할 시스템 기능, 허용되는 운용 조건, 수집해야 할 증거를 명확히 정의해야 한다. 이러한 계획 과정은 시뮬레이션(Simulation), 하드웨어 인 더 루프(HIL), 통합 시험(Integration Testing)과 실제 배치 중심 검증(Deployment-Oriented Validation) 사이를 연결하는 통제된 단계가 된다.

시험 범위(Scope)는 로봇 구성, 소프트웨어 및 펌웨어 버전, 센서 제품군(Sensor Suite), 컴퓨팅 플랫폼(Compute Platform), 탑재물(Payload), 통신 인프라, 시험 환경, 운영자 및 지원 장비를 명시해야 한다. 또한 어떤 기능이 시험 캠페인의 범위에 포함되고 제외되는지를 분명하게 정의해야 한다. 내비게이션(Navigation), 조작(Manipulation), 이동(Locomotion), 인지(Perception), 통신(Communication), 자율성(Autonomy), 안전 기능(Safety Function), 인간 상호작용(Human Interaction)은 서로 다른 시험 조건과 합격 기준을 요구할 수 있다.

효과적인 시험 범위는 정상 운용(Nominal Operation)과 성능 저하 및 비정상 운용(Degraded and Abnormal Operation)을 구분한다. 정상 시험은 의도된 운용 설계 영역(Operational Design Domain)에서 예상되는 동작을 검증하며, 성능 저하 시험에서는 제한된 가시성, 통신 손실, 위치추정 불확실성, 센서 성능 저하, 낮은 배터리 상태 또는 제한된 기동 공간 등의 조건을 통제된 방식으로 적용한다. 비정상 조건은 적절한 격리 및 복구 메커니즘(Containment and Recovery Mechanism)이 확보된 경우에만 시험해야 한다.

각 현장 시험 캠페인은 시스템 요구사항(System Requirements), 식별된 위험요소(Hazards), 이전 검증 결과 또는 해결되지 않은 엔지니어링 위험(Engineering Risk)과 추적 가능한 명시적인 목표를 기반으로 수행해야 한다. 단순히 "내비게이션 성능을 시험한다"는 표현은 지나치게 광범위하다. 보다 명확한 목표는 평가 대상 기능, 운용 조건, 측정 가능한 결과 및 허용 기준을 규정하여 각 시험 실행이 이후 검증, 회귀 분석(Regression Analysis) 또는 인증(Certification)에 활용할 수 있는 증거를 생성하도록 한다.

시험 프로토콜(Test Protocol)은 이러한 목표를 반복 가능한 운용 절차로 변환한다. 각 시험 사례(Test Case)는 초기 조건, 환경 구성, 로봇 상태, 필요한 인력, 계측 장비(Instrumentation), 실행 순서, 예상 동작, 종료 조건 및 기록할 데이터를 설명해야 한다. 프로토콜은 통제되지 않은 변동을 최소화하면서도 현장 시험을 시뮬레이션 및 실험실 검증과 구별하는 실제 환경의 현실성(Environmental Realism)을 유지해야 한다.

구성 관리(Configuration Control)는 시험된 시스템을 다시 재현할 수 있을 때만 현장 시험 결과가 의미를 가지므로 필수적이다. 시험 기록에는 소프트웨어 커밋 또는 릴리스 식별자, 인공지능 모델(AI Model) 버전, 보정 파일(Calibration File), 매개변수 세트(Parameter Set), 펌웨어 개정판, 지도, 임무 정의, 하드웨어 구성 및 관련 인프라 설정을 기록해야 한다. 캠페인 도중 발생한 모든 변경 사항도 기록하고 평가한 후 서로 다른 구성에서 얻어진 결과를 결합해야 한다.

환경 자체도 시험 구성(Test Configuration)의 일부로 관리해야 한다. 지형 형상, 바닥 상태, 경사도, 조명, 날씨, 온도, 장애물, 보행자 활동, 전자기 환경, 위성항법시스템(GNSS) 가용성, 네트워크 커버리지(Network Coverage), 운용 교통 상황은 모두 로봇의 동작에 영향을 줄 수 있다. 따라서 관련 환경 변수(Environmental Variable)를 측정하거나 문서화하여 시스템 고장과 통제되지 않은 시험 조건의 변화를 구별할 수 있어야 한다.

현장 안전 계획(Field Safety Plan)은 로봇의 움직임을 허가하기 전에 수행하는 위험요소 식별(Hazard Identification)에서 시작한다. 잠재적 위험에는 충돌, 압착, 끼임, 추락, 비제어 가속, 액추에이터(Actuator) 오작동, 배터리 사고, 탑재물 낙하, 통신 손실, 불안정한 이동, 예상하지 못한 인공지능 의사결정 및 사람이나 차량과의 상호작용 등이 포함된다. 안전 계획은 각각의 현실적인 위험을 예방 통제, 모니터링 요구사항, 개입 메커니즘 및 비상 대응 절차와 연결해야 한다.

위험 통제(Risk Control)는 운영자의 대응에만 의존하지 않고 다계층 방식(Layered Approach)을 적용해야 한다. 물리적 장벽, 출입 제한 구역(Exclusion Zone), 속도 및 힘 제한, 지오펜싱(Geofencing), 안전 등급 기능(Safety-Rated Function), 비상 정지(Emergency Stop), 원격 비활성화 메커니즘, 보호 장비, 안전 감시자(Spotter), 절차적 통제를 플랫폼과 환경에 따라 조합할 수 있다. 위험도가 높은 시험은 보수적인 제한 조건에서 시작하고 사전에 정의된 준비 조건이 충족된 이후에만 시험 범위를 확대해야 한다.

시험 실행 이전에는 역할(Role)과 권한(Authority)을 명확하게 설정해야 한다. 일반적으로 시험 책임자(Test Director)가 전체 캠페인을 통제하고, 운영자는 로봇을 제어하며, 안전 담당자는 성능 목표와 독립적으로 위험요소를 감시한다. 계측 엔지니어, 관찰자, 유지보수 인력 및 데이터 엔지니어도 시험을 지원할 수 있다. 특히 안전하지 않거나 예상하지 못했거나 충분히 이해되지 않은 상황이 발생했을 때 누가 조건 없이 시험을 중단할 권한을 가지는지 모든 참여자가 명확히 알고 있어야 한다.

시험 전 준비 검토(Pre-Test Readiness Review)는 선행 검증이 완료되었으며 현장 시험 구성이 실제 운용에 적합한지를 확인해야 한다. 여기에는 기계적 무결성, 배터리 상태, 센서 보정, 액추에이터 상태, 위치추정 준비 상태, 네트워크 연결, 데이터 기록 용량, 안전 장치, 비상 정지 기능, 시험 구역 통제, 기상 조건, 인력 간 통신 및 복구 장비의 점검이 포함된다. 준비 항목 중 하나라도 충족되지 않으면 공식적으로 문제가 해결될 때까지 시험 실행을 중단해야 한다.

진행 또는 중단 기준(Go/No-Go Criteria)은 준비 단계와 실제 시험 실행 사이에 객관적인 경계를 제공한다. 인력과 장비가 준비되었다는 이유만으로 시험을 시작해서는 안 된다. 필요한 안전 기능이 정상적으로 작동하고, 환경 조건이 허용 범위 내에 있으며, 지정된 소프트웨어 및 모델 구성이 확인되고, 데이터 수집 시스템이 작동하며, 비상 대응 자원이 준비되어 있어야 한다. 시험 책임자는 이러한 시험 실행 승인 결정을 공식적으로 기록해야 한다.

시험 실행은 승인된 프로토콜을 따라야 하지만 실제 환경에서 발생하는 불확실성에 대해 통제된 방식으로 대응할 수 있어야 한다. 운영자가 예상하지 못한 동작에 대해 임의로 절차를 변경하면 시험 증거의 유효성이 손상되거나 새로운 위험이 발생할 수 있다. 모든 절차 이탈(Deviation)은 발생 시각, 원인, 승인 내용 및 시험에 미치는 영향과 함께 기록해야 한다. 중요한 이탈은 비공식적인 시험 지속이 아니라 시험 종료, 재구성 또는 수정된 시험 사례의 작성으로 이어져야 한다.

특히 자율 로봇(Autonomous Robot)과 인공지능 기반 로봇(AI-Enabled Robot)에서는 명확한 시험 중단 기준(Abort Criteria)이 중요하다. 제한 구역으로의 예상치 못한 진입, 과도한 추종 오차, 불안정한 움직임, 반복적인 인지 실패, 비정상적인 액추에이터 온도, 위치추정 손실, 통신 시간 초과, 안전 모니터 오류, 예상하지 못한 사람의 접근 또는 검증된 운용 범위를 벗어난 행동 등이 중단 조건이 될 수 있다. 안전 결정이 성능 목표에 의해 지연되지 않도록 시험 전에 중단 임계값을 정의해야 한다.

비상 절차(Emergency Procedure)는 중단 명령을 내리는 방법뿐만 아니라 중단 명령 이후 수행해야 하는 조치까지 규정해야 한다. 안전 계획에는 제어 정지(Controlled Stop), 비상 정지, 전원 차단, 불안정한 하드웨어의 안전 확보, 작동 불능 로봇의 회수, 배터리 또는 화재 사고 대응, 책임자 통보 및 증거 보존 방법이 포함되어야 한다. 고에너지, 고속, 항공 또는 사람과 근접한 시험을 수행하기 전에 주요 비상 대응 절차를 사전에 훈련해야 한다.

현장 시험에는 체계적인 데이터 계획(Data Planning)도 필요하다. 시험 캠페인은 각 목표를 평가하기 위해 필요한 텔레메트리(Telemetry), 센서 스트림, 제어 명령, 시스템 상태, 안전 이벤트, 운영자 행동, 타임스탬프(Timestamp), 환경 측정값 및 외부 관찰 정보를 정의해야 한다. 많은 현장 장애는 인지, 계획, 제어, 하드웨어, 네트워크 및 인간 행동의 이벤트를 서로 연관시켜야만 재구성할 수 있으므로 데이터 소스 간 시간 동기화(Time Synchronization)가 매우 중요하다.

합격 및 불합격 기준(Pass/Fail Criteria)은 최종 결과를 분석하기 전에 정의해야 한다. 기준에는 정량적 임계값, 행동 요구사항, 안전 제약조건 및 임무 완료 조건을 함께 적용할 수 있다. 로봇이 임무를 완료하더라도 최소 안전거리 위반, 제어 한계 초과, 승인되지 않은 사람의 개입 또는 위험한 복구 동작이 발생했다면 시험에 실패할 수 있다. 반대로 시스템이 의도한 대로 수행한 통제된 안전 정지는 시험 실패가 아니라 올바른 시스템 동작을 의미할 수 있다.

성능이 확률적인 인공지능 동작, 인지 불확실성, 환경 변동성 또는 인간 상호작용의 영향을 받는 경우 반복 시험(Repeated Trial)이 필요하다. 시험 프로토콜은 하나의 성공적인 시연을 선택하는 대신 성능의 일관성을 평가할 수 있도록 충분한 반복 횟수와 조건 변화를 정의해야 한다. 실패한 시험 역시 성공한 시험과 동일한 수준으로 조건과 결과를 기록해야 하며, 실패 분포(Failure Distribution)는 평균적인 성능 지표만으로는 발견하기 어려운 시스템의 한계를 보여줄 수 있다.

현장 시험 캠페인은 위험도가 낮고 통제된 조건에서 시작하여 점차 실제 운용을 대표하는 조건으로 확장해야 한다. 자율이동로봇(AMR)은 격리된 시험 구역에서 구조화된 장애물 환경을 거쳐 혼합 교통 환경으로 발전시킬 수 있고, 다족 로봇(Legged Robot)은 평탄한 지형에서 불규칙한 표면으로 확장할 수 있다. 휴머노이드(Humanoid)는 제한된 작업에서 인간 상호작용으로, 무인항공기(UAV)는 제한된 비행 영역에서 실제 임무를 대표하는 비행으로 단계적으로 확대할 수 있다.

현장 시험이 종료되었다고 해서 시스템이 자동으로 승인되는 것은 아니다. 시험 실행 후 엔지니어는 데이터 무결성(Data Integrity)을 확인하고, 이상 현상(Anomaly)을 분류하며, 측정 결과를 합격 기준과 비교하고, 시험 프로토콜의 이탈 사항을 확인하며, 추가 시험이 필요한지를 판단해야 한다. 안전 이벤트와 예상하지 못한 동작은 개별 시험을 무효화한다는 이유로 데이터세트에서 제외하지 않고 사고 조사(Incident Investigation)와 근본 원인 분석(Root Cause Analysis)을 위해 보존해야 한다.

잘 설계된 현장 시험 계획은 궁극적으로 요구사항 및 위험에서 시험 프로토콜, 시스템 구성, 실행 기록, 측정 증거 및 엔지니어링 의사결정까지 이어지는 추적성(Traceability)을 형성한다. 이러한 체계는 현장 시험을 단순한 로봇 기능 시연 이상의 과정으로 만든다. 현장 시험은 이후 핵심성과지표(KPI) 분석, 사고 조사, 회귀 시험(Regression Testing), 인증 증거 수집(Certification Evidence Collection), 그리고 시스템이 더 광범위한 실제 배치(Deployment)에 준비되었는지를 판단하기 위한 재현 가능한 검증 프로세스가 된다.

##  

## 05.02. Field Test Environment Setup and Instrumentation

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

Field test environment setup transforms a selected physical location into a controlled and measurable validation space. The objective is not to eliminate real-world variability, but to document and manage it so robot behavior can be interpreted correctly. The environment should reproduce relevant operational conditions while providing sufficient containment, observation, instrumentation, and recovery capability for safe and repeatable testing.

The setup process begins by mapping the intended test objectives to physical requirements. Navigation testing may require representative corridors, intersections, ramps, loading zones, or outdoor paths, while manipulation testing requires controlled workspaces, objects, fixtures, and human interaction zones. Legged robots may require variable terrain, and UAV testing requires defined airspace, launch areas, landing zones, and appropriate safety boundaries.

A field test site should be divided into clearly understood operational zones. These can include the active robot operating area, personnel observation areas, exclusion zones, equipment stations, emergency access paths, and recovery areas. Boundaries should be physically marked where practical and reflected in the robot\'s maps, geofences, or mission configuration so physical and software-defined constraints remain consistent throughout testing.

Before testing, the geometry and physical condition of the environment should be characterized. Relevant properties include dimensions, corridor width, obstacle position, floor friction, surface discontinuities, slopes, stairs, curbs, terrain roughness, ceiling clearance, and available maneuvering space. Accurate characterization allows engineers to determine whether an observed behavior represents a system limitation or simply a change in environmental conditions.

Environmental variables should also be monitored because they can directly affect sensing, computation, communication, and mechanical performance. Illumination, temperature, humidity, precipitation, wind, dust, vibration, acoustic noise, electromagnetic interference, and direct sunlight may alter robot behavior. Outdoor tests may additionally require records of GNSS conditions, weather changes, ground condition, and visibility throughout each test period.

Representative obstacles and interaction elements should be positioned according to the test protocol rather than introduced informally. Static structures, pallets, shelving, vehicles, doors, furniture, vegetation, pedestrians, or movable objects can be used to reproduce operational scenarios. Their initial positions and relevant dimensions should be recorded so repeated trials can distinguish algorithmic variation from unintended changes in the test environment.

Instrumentation converts physical field activity into measurable engineering evidence. The instrumentation architecture should be derived from the questions the test must answer rather than from whichever sensors are easiest to record. Robot telemetry, external reference sensors, environmental measurements, video observations, network traces, operator events, and safety-system states should collectively provide enough information to reconstruct system behavior after the test.

Onboard instrumentation normally captures the robot\'s internal view of the experiment. Typical data includes camera images, LiDAR point clouds, radar observations, IMU measurements, wheel or joint encoders, GNSS data, localization estimates, actuator states, battery measurements, control commands, planner outputs, AI inference results, safety states, diagnostic messages, and system resource utilization. Logging should preserve both inputs and critical derived outputs whenever feasible.

External instrumentation provides an independent reference against which onboard estimates can be evaluated. Depending on the platform and required accuracy, this may include motion-capture systems, survey-grade GNSS, total stations, external cameras, laser trackers, reference IMUs, force measurement equipment, or precisely measured landmarks. Independent ground truth is particularly valuable when testing localization, trajectory accuracy, perception, locomotion, or manipulation performance.

Video recording is a fundamental component of field instrumentation because numerical telemetry alone may not explain physical interactions. Cameras should capture relevant robot motion, surrounding obstacles, people, safety boundaries, and environmental changes. Multiple viewpoints can reduce occlusion and help investigators reconstruct incidents. Video timestamps should be synchronized with robot telemetry so observed physical events can be correlated with internal software decisions.

Time synchronization is one of the most important requirements in a distributed instrumentation system. Cameras, LiDARs, IMUs, robot computers, external measurement systems, network loggers, and operator consoles may otherwise produce timestamps from independent clocks. PTP, GNSS-derived timing, hardware synchronization, or another validated timing method should establish a common temporal reference with accuracy appropriate to the dynamics being measured.

Timestamp provenance should remain understandable throughout the data path. Engineers should know whether a timestamp represents sensor exposure, hardware acquisition, driver reception, middleware publication, application processing, or storage time. Preserving acquisition-time information is especially important when analyzing latency-sensitive failures, because software timestamps generated downstream can hide transport delay, scheduling jitter, buffering, or synchronization errors.

Network instrumentation should characterize communication behavior whenever robot operation depends on wireless or wired connectivity. Relevant measurements can include latency, jitter, packet loss, throughput, signal strength, handover events, connection interruptions, and message timing. For fleet, cloud-connected, teleoperated, or remotely supervised robots, network conditions should be treated as measurable test variables rather than invisible infrastructure assumptions.

Power and thermal instrumentation is important during endurance and high-load testing. Battery voltage, current, state of charge, power consumption, motor temperature, compute temperature, thermal throttling, cooling-system status, and subsystem energy usage can reveal degradation that is not immediately visible in task performance. These measurements are particularly useful when evaluating sustained autonomy, heavy payload operation, high-speed motion, or intensive AI inference.

Instrumentation must not significantly alter the system being evaluated. Additional computers, cameras, storage devices, cables, network traffic, or power loads can change mass distribution, thermal behavior, processor utilization, communication performance, and battery endurance. The test team should therefore evaluate instrumentation intrusiveness and document any measurement equipment that could influence the behavior or performance of the robot.

Data acquisition capacity should be calculated before field execution. High-resolution cameras and LiDARs can generate large data volumes, while AI systems may additionally log intermediate predictions, embeddings, maps, trajectories, and diagnostic information. Storage bandwidth, available capacity, file rotation, compression, transfer procedures, and backup strategy should be verified under representative logging loads before the actual campaign begins.

A structured naming and metadata scheme improves traceability across repeated trials. Each dataset should identify the test campaign, test case, trial number, date and time, robot identifier, hardware and software configuration, AI model version, operator, environment configuration, and relevant conditions. This metadata allows field results to be connected with later data analysis, regression testing, incident investigation, and certification evidence collection.

Instrumentation should undergo its own calibration and verification before it is trusted as evidence. Sensor alignment, camera calibration, measurement scale, coordinate frames, timing accuracy, reference positions, and data channels should be checked using known conditions. Calibration records should be associated with the test campaign because inaccurate reference equipment can create apparently precise but fundamentally incorrect performance conclusions.

Coordinate systems must be defined consistently when measurements originate from multiple devices. Robot base frames, sensor frames, map coordinates, motion-capture coordinates, geographic coordinates, and external camera frames should have documented transformations. Incorrect frame relationships can produce misleading trajectory or localization errors even when every individual sensor is functioning correctly, making coordinate-frame verification a mandatory setup activity.

A dry run should be performed after the environment and instrumentation have been assembled. The robot can execute a low-risk representative sequence while engineers verify sensor visibility, communication coverage, clock synchronization, recording status, safety monitoring, storage throughput, environmental measurements, and external reference systems. A successful dry run demonstrates that the facility can capture the evidence required by the protocol before higher-risk trials begin.

Pre-test checks should confirm that environmental configuration and instrumentation still match the approved setup at the beginning of each session. Obstacles may have moved, wireless conditions may have changed, cameras may have shifted, storage may be nearly full, calibration may have expired, or weather may have moved outside permitted limits. Detecting these changes before execution prevents invalid trials and reduces ambiguity during later analysis.

During testing, operators should monitor both robot behavior and measurement-system health. Loss of a ground-truth sensor, failed logging process, timestamp discontinuity, saturated storage device, disconnected camera, or synchronization fault may invalidate an otherwise successful trial. Instrumentation health should therefore be included in real-time test monitoring and, where evidence is essential, incorporated into predefined abort or repeat criteria.

After each trial, data completeness should be checked before the environment is reconfigured. Engineers should verify that expected logs exist, timestamps cover the full execution period, video files are readable, external reference data was recorded, configuration metadata is preserved, and unusual events have been annotated. Immediate verification is valuable because missing evidence may still be recoverable through a repeated trial while the original conditions remain available.

A well-engineered field environment combines realism with control, while a well-engineered instrumentation system combines comprehensive observation with reliable traceability. Together they provide the foundation for subsequent KPI definition, platform-specific field trials, data analysis, incident investigation, and certification evidence. This relationship is reflected in the chapter sequence, where environment setup and instrumentation precede KPI collection and specialized AMR, quadruped, humanoid, and UAV field testing. Volume_25_Testing_Validation_an...

현장 시험 환경 설정(Field Test Environment Setup)은 선택된 물리적 장소를 통제 가능하고 측정 가능한 검증 공간(Validation Space)으로 전환하는 과정이다. 목적은 실제 환경의 변동성을 제거하는 것이 아니라 이를 문서화하고 관리하여 로봇의 동작을 올바르게 해석할 수 있도록 하는 것이다. 시험 환경은 관련 실제 운용 조건을 재현하는 동시에 안전하고 반복 가능한 시험을 위한 충분한 격리, 관찰, 계측(Instrumentation) 및 복구 능력을 제공해야 한다.

환경 설정 과정은 의도된 시험 목표(Test Objectives)를 물리적 요구사항과 연결하는 것에서 시작한다. 내비게이션 시험(Navigation Testing)에는 대표적인 복도, 교차로, 경사로, 적재 구역 또는 실외 경로가 필요할 수 있으며, 조작 시험(Manipulation Testing)에는 통제된 작업 공간, 물체, 고정 장치 및 인간 상호작용 구역이 필요하다. 다족 로봇(Legged Robot)은 다양한 지형이 필요할 수 있으며, 무인항공기(UAV) 시험에는 정의된 공역, 이륙 구역, 착륙 구역 및 적절한 안전 경계가 필요하다.

현장 시험 장소(Field Test Site)는 명확하게 이해할 수 있는 운용 구역(Operational Zone)으로 구분해야 한다. 여기에는 로봇 활성 운용 구역, 인원 관찰 구역, 출입 제한 구역(Exclusion Zone), 장비 구역, 비상 접근 경로 및 복구 구역이 포함될 수 있다. 가능한 경우 경계를 물리적으로 표시하고 로봇의 지도, 지오펜스(Geofence) 또는 임무 구성에도 반영하여 물리적 제약과 소프트웨어 정의 제약이 시험 전체에서 일관되게 유지되도록 해야 한다.

시험을 시작하기 전에 환경의 기하학적 특성과 물리적 상태를 특성화해야 한다. 관련 속성에는 공간 치수, 복도 폭, 장애물 위치, 바닥 마찰력, 표면 불연속성, 경사, 계단, 연석, 지형 거칠기, 천장 여유 높이 및 사용 가능한 기동 공간 등이 포함된다. 정확한 환경 특성화(Environment Characterization)를 통해 관찰된 로봇 동작이 시스템 자체의 한계인지 단순한 환경 조건 변화의 결과인지를 판단할 수 있다.

환경 변수(Environmental Variables)는 센싱, 연산, 통신 및 기계적 성능에 직접적인 영향을 줄 수 있으므로 지속적으로 관찰해야 한다. 조도, 온도, 습도, 강수량, 바람, 먼지, 진동, 음향 소음, 전자기 간섭(Electromagnetic Interference), 직사광선 등이 로봇의 동작을 변화시킬 수 있다. 실외 시험에서는 각 시험 기간 동안 위성항법시스템(GNSS) 상태, 기상 변화, 지면 상태 및 가시성에 대한 기록도 추가로 필요할 수 있다.

대표적인 장애물과 상호작용 요소는 비공식적으로 배치하는 것이 아니라 시험 프로토콜(Test Protocol)에 따라 배치해야 한다. 고정 구조물, 팔레트, 선반, 차량, 문, 가구, 식생, 보행자 또는 이동 가능한 물체 등을 사용하여 실제 운용 시나리오를 재현할 수 있다. 초기 위치와 관련 치수를 기록하여 반복 시험에서 발생하는 알고리즘의 변동과 의도하지 않은 시험 환경의 변화를 구별할 수 있도록 해야 한다.

계측(Instrumentation)은 물리적인 현장 활동을 측정 가능한 엔지니어링 증거(Engineering Evidence)로 변환한다. 계측 아키텍처(Instrumentation Architecture)는 단순히 기록하기 쉬운 센서를 기준으로 구성하는 것이 아니라 시험에서 해결해야 할 질문을 기준으로 설계해야 한다. 로봇 텔레메트리(Robot Telemetry), 외부 기준 센서, 환경 측정값, 영상 관찰, 네트워크 추적(Network Trace), 운영자 이벤트 및 안전 시스템 상태를 종합하여 시험 이후 시스템 동작을 재구성할 수 있는 충분한 정보를 확보해야 한다.

온보드 계측(Onboard Instrumentation)은 일반적으로 시험에 대한 로봇 내부 관점의 데이터를 수집한다. 대표적인 데이터에는 카메라 영상, 라이다(LiDAR) 포인트 클라우드, 레이더 관측값, 관성측정장치(IMU) 측정값, 휠 또는 관절 엔코더, 위성항법시스템(GNSS) 데이터, 위치추정 결과, 액추에이터 상태, 배터리 측정값, 제어 명령, 플래너(Planner) 출력, 인공지능 추론(AI Inference) 결과, 안전 상태, 진단 메시지 및 시스템 자원 사용량 등이 포함된다. 가능한 경우 입력 데이터와 주요 파생 출력을 모두 보존해야 한다.

외부 계측(External Instrumentation)은 온보드 추정값을 평가할 수 있는 독립적인 기준 정보를 제공한다. 플랫폼과 요구 정확도에 따라 모션 캡처 시스템(Motion Capture System), 측량 등급 위성항법시스템(Survey-Grade GNSS), 토털 스테이션(Total Station), 외부 카메라, 레이저 트래커(Laser Tracker), 기준 관성측정장치, 힘 측정 장비 또는 정밀하게 측정된 랜드마크를 사용할 수 있다. 독립적인 정답 데이터(Ground Truth)는 위치추정, 궤적 정확도, 인지, 이동 또는 조작 성능을 시험할 때 특히 중요하다.

영상 기록(Video Recording)은 수치형 텔레메트리만으로 물리적 상호작용을 완전히 설명하기 어려울 수 있기 때문에 현장 계측의 핵심 요소이다. 카메라는 로봇의 주요 움직임, 주변 장애물, 사람, 안전 경계 및 환경 변화를 기록해야 한다. 여러 시점에서 촬영하면 가려짐(Occlusion)을 줄이고 사고 재구성에 도움을 줄 수 있다. 영상의 타임스탬프는 로봇 텔레메트리와 동기화하여 실제 물리적 사건을 내부 소프트웨어의 의사결정과 연계할 수 있어야 한다.

시간 동기화(Time Synchronization)는 분산 계측 시스템(Distributed Instrumentation System)에서 가장 중요한 요구사항 중 하나이다. 카메라, 라이다, 관성측정장치, 로봇 컴퓨터, 외부 측정 시스템, 네트워크 로거(Network Logger), 운영자 콘솔이 서로 독립적인 시계를 사용하면 서로 다른 타임스탬프가 생성될 수 있다. 정밀 시간 프로토콜(PTP), GNSS 기반 시간, 하드웨어 동기화 또는 검증된 다른 시간 동기화 방식을 사용하여 측정 대상의 동적 특성에 적합한 정확도의 공통 시간 기준(Common Temporal Reference)을 구축해야 한다.

타임스탬프 출처(Timestamp Provenance)는 전체 데이터 경로에서 명확하게 파악할 수 있어야 한다. 엔지니어는 타임스탬프가 센서 노출 시점, 하드웨어 획득 시점, 드라이버 수신 시점, 미들웨어 발행 시점, 애플리케이션 처리 시점 또는 저장 시점을 의미하는지 알아야 한다. 특히 지연시간에 민감한 장애를 분석할 때 획득 시점 정보를 보존하는 것이 중요하며, 후단에서 생성된 소프트웨어 타임스탬프는 전송 지연, 스케줄링 지터(Scheduling Jitter), 버퍼링 또는 동기화 오류를 감출 수 있다.

로봇 운용이 유선 또는 무선 연결에 의존한다면 네트워크 계측(Network Instrumentation)을 통해 통신 동작을 특성화해야 한다. 관련 측정값에는 지연시간(Latency), 지터(Jitter), 패킷 손실(Packet Loss), 처리량(Throughput), 신호 강도, 핸드오버 이벤트, 연결 중단 및 메시지 타이밍 등이 포함될 수 있다. 플릿(Fleet), 클라우드 연결, 원격조작(Teleoperation) 또는 원격 감독 로봇에서는 네트워크 상태를 보이지 않는 인프라 가정으로 취급하지 않고 측정 가능한 시험 변수로 관리해야 한다.

전력 및 열 계측(Power and Thermal Instrumentation)은 내구 시험과 고부하 시험에서 중요하다. 배터리 전압, 전류, 충전 상태(State of Charge), 전력 소비량, 모터 온도, 컴퓨팅 장치 온도, 열 스로틀링(Thermal Throttling), 냉각 시스템 상태 및 하위 시스템별 에너지 사용량은 작업 성능만으로 즉시 확인하기 어려운 성능 저하를 보여줄 수 있다. 이러한 측정은 장시간 자율 운용, 고중량 탑재물 운용, 고속 이동 또는 고부하 인공지능 추론을 평가할 때 특히 유용하다.

계측 장비 자체가 평가 대상 시스템에 큰 영향을 주어서는 안 된다. 추가 컴퓨터, 카메라, 저장장치, 케이블, 네트워크 트래픽 또는 전력 부하는 질량 분포, 열 특성, 프로세서 사용률, 통신 성능 및 배터리 지속시간을 변화시킬 수 있다. 따라서 시험팀은 계측의 침습성(Instrumentation Intrusiveness)을 평가하고 로봇의 동작이나 성능에 영향을 줄 가능성이 있는 모든 측정 장비를 문서화해야 한다.

현장 시험 실행 전에 데이터 수집 용량(Data Acquisition Capacity)을 계산해야 한다. 고해상도 카메라와 라이다는 대규모 데이터를 생성하며, 인공지능 시스템은 중간 예측 결과, 임베딩(Embedding), 지도, 궤적 및 진단 정보까지 추가로 기록할 수 있다. 실제 시험 캠페인을 시작하기 전에 대표적인 기록 부하를 적용하여 저장 대역폭, 사용 가능한 저장 용량, 파일 순환(File Rotation), 압축, 데이터 전송 절차 및 백업 전략이 정상적으로 작동하는지 검증해야 한다.

구조화된 명명 규칙과 메타데이터 체계(Metadata Scheme)는 반복 시험 간 추적성(Traceability)을 향상시킨다. 각 데이터세트에는 시험 캠페인, 시험 사례, 시험 횟수, 날짜와 시간, 로봇 식별자, 하드웨어 및 소프트웨어 구성, 인공지능 모델 버전, 운영자, 환경 구성 및 관련 시험 조건을 기록해야 한다. 이러한 메타데이터를 통해 현장 시험 결과를 이후 데이터 분석, 회귀 시험(Regression Testing), 사고 조사 및 인증 증거 수집과 연결할 수 있다.

계측 시스템은 증거로 신뢰하기 전에 자체적인 보정(Calibration)과 검증을 수행해야 한다. 센서 정렬, 카메라 보정, 측정 스케일, 좌표 프레임(Coordinate Frame), 시간 정확도, 기준 위치 및 데이터 채널을 알려진 조건을 이용하여 점검해야 한다. 부정확한 기준 장비는 겉보기에는 정밀하지만 근본적으로 잘못된 성능 결론을 만들 수 있으므로 보정 기록을 해당 시험 캠페인과 연계하여 관리해야 한다.

여러 장치에서 측정값을 획득하는 경우 좌표계(Coordinate System)를 일관되게 정의해야 한다. 로봇 베이스 프레임(Base Frame), 센서 프레임, 지도 좌표, 모션 캡처 좌표, 지리 좌표 및 외부 카메라 프레임 사이의 변환 관계를 문서화해야 한다. 개별 센서가 모두 정상적으로 작동하더라도 프레임 간 관계가 잘못되면 잘못된 궤적 또는 위치추정 오차가 발생할 수 있으므로 좌표 프레임 검증은 필수적인 환경 설정 작업이다.

환경과 계측 시스템의 구성이 완료되면 예비 실행(Dry Run)을 수행해야 한다. 로봇이 위험도가 낮은 대표적인 동작을 수행하는 동안 엔지니어는 센서 가시성, 통신 커버리지, 시계 동기화, 기록 상태, 안전 모니터링, 저장 처리량, 환경 측정 및 외부 기준 시스템을 확인할 수 있다. 성공적인 예비 실행은 위험도가 높은 시험을 시작하기 전에 시험 시설이 프로토콜에서 요구하는 증거를 정상적으로 수집할 수 있음을 입증한다.

각 시험 세션을 시작할 때 시험 전 점검(Pre-Test Check)을 수행하여 환경 구성과 계측 상태가 승인된 설정과 여전히 일치하는지 확인해야 한다. 장애물이 이동했거나, 무선 통신 조건이 변경되었거나, 카메라 위치가 변했거나, 저장 공간이 부족하거나, 보정 유효기간이 지났거나, 기상 조건이 허용 범위를 벗어났을 수 있다. 이러한 변화를 시험 실행 전에 발견하면 무효 시험을 방지하고 이후 분석 과정에서 발생하는 모호성을 줄일 수 있다.

시험 중 운영자는 로봇의 동작뿐만 아니라 측정 시스템의 상태(Measurement-System Health)도 지속적으로 감시해야 한다. 정답 센서(Ground-Truth Sensor)의 손실, 데이터 기록 프로세스 실패, 타임스탬프 불연속, 저장장치 포화, 카메라 연결 해제 또는 동기화 장애가 발생하면 로봇이 성공적으로 임무를 수행했더라도 해당 시험은 무효가 될 수 있다. 따라서 계측 시스템의 상태를 실시간 시험 모니터링에 포함하고 핵심 증거가 필요한 경우 사전에 정의된 시험 중단 또는 재시험 기준에도 반영해야 한다.

각 시험이 종료된 후 환경을 재구성하기 전에 데이터 완전성(Data Completeness)을 확인해야 한다. 엔지니어는 예상된 로그가 존재하는지, 타임스탬프가 전체 시험 실행 구간을 포함하는지, 영상 파일을 정상적으로 읽을 수 있는지, 외부 기준 데이터가 기록되었는지, 구성 메타데이터가 보존되었는지, 비정상적인 이벤트가 주석 처리되었는지를 검증해야 한다. 즉각적인 확인은 기존 시험 조건이 유지되는 동안 누락된 증거를 재시험을 통해 확보할 수 있다는 점에서 중요하다.

잘 설계된 현장 환경(Field Environment)은 현실성과 통제 가능성을 결합하고, 잘 설계된 계측 시스템(Instrumentation System)은 포괄적인 관찰 능력과 신뢰할 수 있는 추적성을 결합한다. 이 두 요소는 이후 핵심성과지표(KPI) 정의, 플랫폼별 현장 시험, 데이터 분석, 사고 조사 및 인증 증거 수집을 위한 기반을 제공한다. 따라서 현장 시험 환경과 계측의 체계적인 구축은 자율이동로봇(AMR), 다족 로봇, 휴머노이드(Humanoid), 무인항공기(UAV)와 같은 다양한 로봇 플랫폼의 실제 환경 검증을 수행하기 위한 핵심 선행 단계이다.

##  

## 05.03. KPI Definition and Data Collection in Field [w/Code]

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

Key Performance Indicators should translate field-test objectives into measurable evidence of whether a robot performs its intended mission safely, reliably, and efficiently. A useful KPI is tied to a requirement or engineering question, has a precise definition and unit, identifies the population of events being measured, and specifies an acceptance threshold. Field KPIs should describe operational performance rather than merely report raw sensor values.

KPI selection should begin with the mission and platform rather than with available telemetry. An AMR may emphasize mission success, localization accuracy, obstacle avoidance, travel time, intervention frequency, and energy consumption. A quadruped may require stability and terrain metrics, while humanoid, manipulation, and UAV systems need task-specific measures. Common system-level KPIs can still provide a basis for comparing releases and configurations.

Each KPI should have an operational definition that removes ambiguity from later analysis. A mission success rate, for example, requires explicit definitions of mission start, successful completion, timeout, abort, operator intervention, and invalid trial. Localization error must specify the reference system, coordinate frame, sampling interval, and error statistic. Without such definitions, different teams can calculate apparently identical KPIs and obtain incompatible results.

KPIs should be organized around dimensions such as effectiveness, accuracy, safety, robustness, efficiency, reliability, and operational continuity. Effectiveness measures whether the robot accomplishes its task, while accuracy measures how closely behavior follows the desired state. Safety KPIs capture hazardous proximity or protective interventions, and efficiency metrics describe time, distance, computation, energy, or other resources consumed during execution.

Field evaluation should distinguish outcome KPIs from diagnostic metrics. Task completion rate and collision rate describe externally meaningful outcomes, whereas CPU utilization, perception latency, localization covariance, motor current, or packet loss help explain why those outcomes occurred. Both categories are necessary. Outcome metrics support acceptance decisions, while diagnostic measurements provide engineering context for root-cause analysis and performance improvement.

Safety KPIs should measure more than the absence of accidents. Useful indicators may include minimum separation distance, emergency-stop activation frequency, protective-stop events, speed-limit violations, geofence violations, near-miss events, human interventions, and time required to reach a safe state. A test campaign should preserve these events even when the mission itself is completed successfully because task success does not override safety requirements.

Reliability KPIs characterize whether performance remains consistent over repeated operation. Relevant measures can include successful missions per operating hour, failure frequency, recovery success rate, mean time between operational failures, software restart frequency, sensor dropout events, and autonomous operation duration. Long-duration field trials are especially important because thermal, battery, communication, mechanical, and software-state problems may not appear during short demonstrations.

Efficiency KPIs quantify the resources required to achieve useful behavior. Travel distance relative to a reference route, mission completion time, energy consumed per mission, battery discharge per kilometer, compute utilization, communication bandwidth, idle time, and charging requirements can reveal performance differences that success rate alone cannot show. Efficiency metrics become particularly important when evaluating deployment economics or fleet-scale operation.

Data collection should be designed directly from the KPI definitions. For every KPI, engineers should identify the source signals, sampling requirements, units, timestamps, reference measurements, environmental metadata, and processing method required to calculate it. This approach prevents a common field-testing failure in which large volumes of telemetry are collected but the specific information required to answer the validation question is missing.

Field data normally combines multiple sources rather than relying on a single robot log. Onboard sensor streams, localization and planning outputs, actuator telemetry, safety-controller states, diagnostic messages, external ground-truth systems, environmental sensors, network measurements, operator annotations, and synchronized video may all contribute to KPI calculation. Their relationships should be defined before execution so the analysis pipeline can reconstruct each trial consistently.

A standardized event model makes field datasets easier to analyze. Events such as mission_start, goal_reached, obstacle_detected, replanning_started, localization_lost, operator_intervention, protective_stop, emergency_stop, recovery_started, and mission_end can be recorded with timestamps and contextual attributes. Consistent event semantics enable automatic calculation of durations, frequencies, transition sequences, and failure categories across large collections of field trials.

Time synchronization is critical when KPI calculation combines distributed data sources. A braking-response metric may require correlation among obstacle detection, perception output, planner decision, controller command, actuator response, and external motion measurement. Even small clock offsets can distort latency or stopping-distance analysis. Data pipelines should therefore preserve synchronized acquisition timestamps and document the timing source and expected synchronization accuracy.

Sampling frequency should match the dynamics of the quantity being evaluated. Environmental temperature may require relatively slow sampling, whereas vibration, control response, impact events, or fast vehicle motion may require much higher rates. Excessive downsampling can hide short-duration failures, while unnecessarily high sampling increases storage and processing cost. Sampling policies should therefore follow the temporal resolution required by each KPI.

Data quality should itself be monitored during collection. Missing samples, corrupted messages, timestamp reversals, duplicate records, sensor saturation, dropped frames, invalid coordinate transformations, and synchronization loss can bias KPI calculations. Automated quality checks should flag incomplete intervals and distinguish valid system failures from failures of the measurement infrastructure. Invalid data should never be silently converted into apparently normal performance statistics.

Context metadata is essential because field performance depends strongly on operating conditions. Each trial should preserve robot configuration, software release, AI model version, map, payload, battery state, operator, environment identifier, weather, lighting, terrain, traffic density, network condition, and other relevant factors. This metadata enables engineers to stratify KPI results and determine whether degradation is associated with a particular configuration or operating condition.

Repeated trials should capture both central performance and variability. Reporting only an average can hide unstable behavior, rare failures, or long-tail latency. Depending on the KPI, analysis may include median values, percentiles, standard deviation, confidence intervals, minimum and maximum values, failure distributions, or success proportions. The selected statistics should reflect the operational consequence of variation rather than being chosen solely for convenience.

KPIs should also be analyzed by scenario instead of being aggregated indiscriminately. A navigation system with a high overall success rate may perform poorly at narrow intersections, reflective surfaces, crowded areas, ramps, or low-light locations. Scenario labels allow engineers to identify these weaknesses. Environmental and operational dimensions therefore become part of KPI interpretation and help connect field observations with simulation and regression scenarios.

Thresholds should be defined before final analysis whenever the KPI supports an acceptance decision. A threshold may originate from a system requirement, safety constraint, customer objective, benchmark, or engineering baseline. Some metrics use a single pass/fail boundary, while others require warning and critical ranges. Predefined thresholds reduce the risk of changing evaluation criteria after observing results and make comparisons between releases more defensible.

Operator intervention requires explicit treatment because it can artificially improve apparent robot performance. The dataset should distinguish autonomous success, assisted success, recovery after intervention, and unsuccessful completion. Intervention reason, duration, and type should be recorded. A robot that completes every mission but frequently requires human correction represents a substantially different autonomy level from one achieving the same completion rate without assistance.

Failures and near misses are particularly valuable data rather than records to discard. They should be tagged with reproducible categories describing perception, localization, planning, control, hardware, communication, safety, human interaction, environment, or unknown causes. Such classification supports later root-cause analysis and helps transform field observations into new simulation scenarios, regression tests, fault-injection cases, and engineering requirements.

The field-data pipeline should preserve raw evidence while also producing analysis-ready datasets. Raw sensor and event records provide the basis for later reprocessing when algorithms or hypotheses change, whereas normalized tables and derived metrics support efficient comparison. Processing steps, filtering rules, coordinate transformations, excluded intervals, and KPI formulas should be version-controlled so results can be reproduced after the campaign.

Automated KPI computation reduces manual inconsistency and supports repeated campaigns. Analysis software can ingest trial metadata and synchronized logs, detect standardized events, calculate metrics, evaluate thresholds, and generate per-trial and aggregate results. The same calculation logic should be applied across software versions whenever possible so performance trends reflect changes in the robot rather than changes in the evaluation procedure.

A complete KPI dataset should maintain traceability from the original field trial to the reported result. Engineers should be able to identify which robot configuration, log files, environmental conditions, processing version, reference data, and calculation method produced a particular value. This traceability becomes important when a metric is used for release approval, safety review, regression assessment, incident investigation, or certification evidence.

Effective KPI definition and field data collection therefore form a closed measurement discipline rather than two independent activities. The KPI determines what evidence must be captured, instrumentation supplies that evidence, and the data pipeline converts it into reproducible engineering conclusions. Within the field-testing methodology, this provides the quantitative foundation for subsequent AMR, quadruped, humanoid, and UAV field evaluations and later logging and analysis activities.

핵심성과지표(KPI)는 현장 시험 목표(Field-Test Objectives)를 로봇이 의도된 임무를 안전하고 신뢰성 있으며 효율적으로 수행하는지를 판단할 수 있는 측정 가능한 증거로 변환해야 한다. 유용한 핵심성과지표는 요구사항 또는 엔지니어링 질문과 연결되고, 정확한 정의와 단위를 가지며, 측정 대상 이벤트의 모집단을 명확히 하고, 허용 기준(Acceptance Threshold)을 규정해야 한다. 현장 핵심성과지표는 단순한 원시 센서 값이 아니라 실제 운용 성능을 설명해야 한다.

핵심성과지표 선정(KPI Selection)은 사용 가능한 텔레메트리(Telemetry)가 아니라 임무와 플랫폼을 기준으로 시작해야 한다. 자율이동로봇(AMR)은 임무 성공률, 위치추정 정확도, 장애물 회피, 이동 시간, 개입 빈도 및 에너지 소비를 중요하게 평가할 수 있다. 사족보행 로봇(Quadruped)은 안정성과 지형 관련 지표가 필요하며, 휴머노이드(Humanoid), 조작(Manipulation), 무인항공기(UAV) 시스템에는 작업별 지표가 필요하다. 동시에 공통 시스템 수준 핵심성과지표를 사용하면 릴리스와 구성 간 비교 기준을 확보할 수 있다.

각 핵심성과지표는 이후 분석 과정의 모호성을 제거할 수 있는 운용 정의(Operational Definition)를 가져야 한다. 예를 들어 임무 성공률(Mission Success Rate)은 임무 시작, 성공적인 완료, 시간 초과, 중단, 운영자 개입 및 무효 시험을 명확히 정의해야 한다. 위치추정 오차(Localization Error)는 기준 시스템, 좌표 프레임(Coordinate Frame), 샘플링 간격 및 오차 통계량을 규정해야 한다. 이러한 정의가 없으면 서로 다른 팀이 동일해 보이는 지표를 계산하면서도 서로 호환되지 않는 결과를 얻을 수 있다.

핵심성과지표는 효과성(Effectiveness), 정확도(Accuracy), 안전성(Safety), 강건성(Robustness), 효율성(Efficiency), 신뢰성(Reliability), 운용 연속성(Operational Continuity)과 같은 차원을 중심으로 구성해야 한다. 효과성은 로봇이 작업을 달성하는지를 측정하고, 정확도는 실제 동작이 목표 상태에 얼마나 근접하는지를 평가한다. 안전 핵심성과지표는 위험한 근접이나 보호 개입을 측정하며, 효율성 지표는 실행 과정에서 소비되는 시간, 거리, 연산량, 에너지 또는 기타 자원을 설명한다.

현장 평가는 결과 핵심성과지표(Outcome KPI)와 진단 지표(Diagnostic Metric)를 구분해야 한다. 작업 완료율과 충돌률은 외부적으로 의미 있는 결과를 나타내지만, 중앙처리장치(CPU) 사용률, 인지 지연시간, 위치추정 공분산(Localization Covariance), 모터 전류 또는 패킷 손실은 그러한 결과가 발생한 원인을 설명하는 데 도움을 준다. 두 범주 모두 필요하며, 결과 지표는 승인 의사결정을 지원하고 진단 측정값은 근본 원인 분석(Root-Cause Analysis)과 성능 개선을 위한 엔지니어링 맥락을 제공한다.

안전 핵심성과지표(Safety KPI)는 단순히 사고가 발생하지 않았다는 사실 이상을 측정해야 한다. 유용한 지표에는 최소 이격 거리, 비상 정지(Emergency Stop) 작동 빈도, 보호 정지(Protective Stop) 이벤트, 속도 제한 위반, 지오펜스(Geofence) 위반, 아차 사고(Near-Miss) 이벤트, 인간 개입 및 안전 상태에 도달하는 데 필요한 시간 등이 포함될 수 있다. 임무가 성공적으로 완료되었더라도 작업 성공이 안전 요구사항보다 우선할 수 없으므로 이러한 이벤트를 반드시 보존해야 한다.

신뢰성 핵심성과지표(Reliability KPI)는 반복적인 운용에서 성능이 얼마나 일관되게 유지되는지를 평가한다. 관련 측정값에는 운용 시간당 성공 임무 수, 장애 빈도, 복구 성공률, 운용 장애 간 평균 시간, 소프트웨어 재시작 빈도, 센서 데이터 손실 이벤트 및 자율 운용 지속시간 등이 포함될 수 있다. 특히 열, 배터리, 통신, 기계 및 소프트웨어 상태와 관련된 문제는 짧은 시연에서 나타나지 않을 수 있으므로 장시간 현장 시험(Long-Duration Field Trial)이 중요하다.

효율성 핵심성과지표(Efficiency KPI)는 유용한 동작을 달성하는 데 필요한 자원을 정량화한다. 기준 경로 대비 이동 거리, 임무 완료 시간, 임무당 에너지 소비량, 킬로미터당 배터리 소모량, 컴퓨팅 자원 사용률, 통신 대역폭, 유휴 시간 및 충전 요구사항은 성공률만으로 확인하기 어려운 성능 차이를 보여줄 수 있다. 효율성 지표는 실제 배치 경제성(Deployment Economics) 또는 대규모 플릿 운용(Fleet-Scale Operation)을 평가할 때 특히 중요하다.

데이터 수집(Data Collection)은 핵심성과지표의 정의에서 직접 도출하여 설계해야 한다. 각각의 핵심성과지표에 대해 엔지니어는 계산에 필요한 원천 신호(Source Signal), 샘플링 요구사항, 단위, 타임스탬프(Timestamp), 기준 측정값, 환경 메타데이터(Environmental Metadata) 및 처리 방법을 식별해야 한다. 이러한 접근법은 방대한 양의 텔레메트리를 수집했지만 실제 검증 질문에 답하는 데 필요한 특정 정보가 누락되는 일반적인 현장 시험 실패를 방지한다.

현장 데이터(Field Data)는 일반적으로 단일 로봇 로그에 의존하지 않고 여러 데이터 소스를 결합한다. 온보드 센서 스트림, 위치추정 및 계획 출력, 액추에이터 텔레메트리, 안전 제어기 상태, 진단 메시지, 외부 정답 시스템(Ground-Truth System), 환경 센서, 네트워크 측정값, 운영자 주석 및 동기화된 영상 등이 핵심성과지표 계산에 사용될 수 있다. 분석 파이프라인(Analysis Pipeline)이 각 시험을 일관되게 재구성할 수 있도록 이러한 데이터 간 관계를 시험 실행 전에 정의해야 한다.

표준화된 이벤트 모델(Standardized Event Model)은 현장 데이터세트의 분석을 용이하게 한다. 임무 시작(mission_start), 목표 도달(goal_reached), 장애물 감지(obstacle_detected), 재계획 시작(replanning_started), 위치추정 손실(localization_lost), 운영자 개입(operator_intervention), 보호 정지(protective_stop), 비상 정지(emergency_stop), 복구 시작(recovery_started), 임무 종료(mission_end) 등의 이벤트를 타임스탬프와 상황 속성(Contextual Attributes)과 함께 기록할 수 있다. 일관된 이벤트 의미체계(Event Semantics)는 대규모 현장 시험에서 지속시간, 빈도, 상태 전이 순서 및 장애 유형을 자동으로 계산할 수 있게 한다.

핵심성과지표 계산에서 분산된 데이터 소스를 결합하는 경우 시간 동기화(Time Synchronization)가 매우 중요하다. 제동 응답 지표를 계산하려면 장애물 감지, 인지 출력, 플래너(Planner) 결정, 제어기 명령, 액추에이터 응답 및 외부 움직임 측정값을 서로 연계해야 할 수 있다. 작은 시계 오차도 지연시간이나 정지거리 분석을 왜곡할 수 있으므로 데이터 파이프라인은 동기화된 획득 타임스탬프를 보존하고 시간 기준과 예상 동기화 정확도를 문서화해야 한다.

샘플링 주파수(Sampling Frequency)는 평가 대상 물리량의 동적 특성에 적합해야 한다. 환경 온도는 상대적으로 낮은 주파수의 샘플링으로 충분할 수 있지만, 진동, 제어 응답, 충격 이벤트 또는 고속 차량 움직임은 훨씬 높은 샘플링 속도를 요구할 수 있다. 과도한 다운샘플링(Downsampling)은 짧은 시간 동안 발생하는 장애를 숨길 수 있으며, 불필요하게 높은 샘플링은 저장 및 처리 비용을 증가시킨다. 따라서 각 핵심성과지표가 요구하는 시간 해상도(Temporal Resolution)를 기준으로 샘플링 정책을 결정해야 한다.

데이터 품질(Data Quality) 자체도 수집 과정에서 지속적으로 감시해야 한다. 누락된 샘플, 손상된 메시지, 타임스탬프 역전, 중복 레코드, 센서 포화, 프레임 손실, 잘못된 좌표 변환 및 동기화 손실은 핵심성과지표 계산 결과에 편향을 발생시킬 수 있다. 자동화된 품질 검사(Automated Quality Check)를 통해 불완전한 구간을 표시하고 실제 시스템 장애와 측정 인프라의 장애를 구분해야 한다. 유효하지 않은 데이터를 정상적인 성능 통계로 조용히 변환해서는 안 된다.

현장 성능은 운용 조건에 크게 의존하므로 상황 메타데이터(Context Metadata)가 필수적이다. 각 시험에는 로봇 구성, 소프트웨어 릴리스, 인공지능 모델(AI Model) 버전, 지도, 탑재물(Payload), 배터리 상태, 운영자, 환경 식별자, 날씨, 조명, 지형, 교통 밀도, 네트워크 상태 및 기타 관련 요소를 보존해야 한다. 이러한 메타데이터를 활용하면 핵심성과지표 결과를 조건별로 계층화하고 특정 구성이나 운용 조건과 성능 저하 사이의 연관성을 분석할 수 있다.

반복 시험(Repeated Trial)은 대표적인 성능뿐만 아니라 성능 변동성(Variability)도 포착해야 한다. 평균값만 보고하면 불안정한 동작, 드문 장애 또는 긴 꼬리 지연시간(Long-Tail Latency)을 숨길 수 있다. 핵심성과지표에 따라 중앙값, 백분위수(Percentile), 표준편차, 신뢰구간, 최솟값과 최댓값, 장애 분포 또는 성공 비율 등을 분석할 수 있다. 통계 방법은 단순한 계산 편의성이 아니라 성능 변동이 실제 운용에 미치는 영향을 기준으로 선택해야 한다.

핵심성과지표는 모든 결과를 무차별적으로 통합하기보다 시나리오(Scenario)별로 분석해야 한다. 전체적으로 높은 성공률을 가진 내비게이션 시스템도 좁은 교차로, 반사 표면, 혼잡 지역, 경사로 또는 저조도 환경에서는 낮은 성능을 보일 수 있다. 시나리오 레이블(Scenario Label)을 사용하면 이러한 취약점을 식별할 수 있다. 따라서 환경 및 운용 조건은 핵심성과지표 해석의 일부가 되며 현장 관찰 결과를 시뮬레이션 및 회귀 시험 시나리오와 연결하는 데 도움을 준다.

핵심성과지표가 승인 의사결정에 사용되는 경우 가능한 한 최종 분석 전에 임계값(Threshold)을 정의해야 한다. 임계값은 시스템 요구사항, 안전 제약조건, 고객 목표, 벤치마크(Benchmark) 또는 엔지니어링 기준선(Engineering Baseline)에서 도출할 수 있다. 일부 지표는 하나의 합격 및 불합격 경계를 사용하지만 다른 지표는 경고와 위험 범위를 별도로 요구할 수 있다. 사전에 정의된 임계값은 결과를 확인한 이후 평가 기준을 변경하는 위험을 줄이고 릴리스 간 비교의 객관성을 높인다.

운영자 개입(Operator Intervention)은 로봇의 실제 성능을 인위적으로 높게 보이게 할 수 있으므로 명시적으로 처리해야 한다. 데이터세트는 완전 자율 성공, 지원을 통한 성공, 개입 이후 복구 및 임무 완료 실패를 구분해야 한다. 또한 개입 원인, 지속시간 및 유형을 기록해야 한다. 모든 임무를 완료하지만 빈번하게 사람의 수정이 필요한 로봇은 동일한 임무 완료율을 사람의 도움 없이 달성하는 로봇과 본질적으로 다른 자율성 수준(Autonomy Level)을 가진다.

장애(Failure)와 아차 사고(Near Miss)는 폐기해야 할 기록이 아니라 특히 가치가 높은 데이터이다. 이러한 사례는 인지, 위치추정, 계획, 제어, 하드웨어, 통신, 안전, 인간 상호작용, 환경 또는 원인 불명과 같은 재현 가능한 범주로 분류해야 한다. 이러한 분류는 이후 근본 원인 분석을 지원하며 현장 관찰 결과를 새로운 시뮬레이션 시나리오, 회귀 시험, 결함 주입 시험(Fault-Injection Test) 및 엔지니어링 요구사항으로 전환하는 데 활용할 수 있다.

현장 데이터 파이프라인(Field-Data Pipeline)은 원시 증거(Raw Evidence)를 보존하는 동시에 분석 준비 데이터세트(Analysis-Ready Dataset)를 생성해야 한다. 원시 센서 및 이벤트 기록은 알고리즘이나 분석 가설이 변경되었을 때 데이터를 다시 처리할 수 있는 기반을 제공하며, 정규화된 테이블과 파생 지표(Derived Metric)는 효율적인 비교를 지원한다. 처리 단계, 필터링 규칙, 좌표 변환, 제외 구간 및 핵심성과지표 계산식은 버전 관리(Version Control)하여 시험 이후에도 결과를 재현할 수 있어야 한다.

자동화된 핵심성과지표 계산(Automated KPI Computation)은 수작업에 따른 불일치를 줄이고 반복적인 시험 캠페인을 지원한다. 분석 소프트웨어는 시험 메타데이터와 동기화된 로그를 입력받아 표준화된 이벤트를 탐지하고, 지표를 계산하고, 임계값을 평가하며, 개별 시험과 전체 시험에 대한 결과를 생성할 수 있다. 가능한 경우 소프트웨어 버전이 변경되더라도 동일한 계산 로직을 적용하여 성능 추세가 평가 절차의 변화가 아니라 실제 로봇 성능의 변화를 반영하도록 해야 한다.

완전한 핵심성과지표 데이터세트(KPI Dataset)는 최초 현장 시험에서 최종 보고 결과까지의 추적성을 유지해야 한다. 엔지니어는 특정 지표 값이 어떤 로봇 구성, 로그 파일, 환경 조건, 처리 버전, 기준 데이터 및 계산 방법으로부터 생성되었는지 확인할 수 있어야 한다. 이러한 추적성은 해당 지표가 릴리스 승인, 안전성 검토, 회귀 평가, 사고 조사 또는 인증 증거(Certification Evidence)로 사용될 때 특히 중요하다.

효과적인 핵심성과지표 정의와 현장 데이터 수집은 서로 독립적인 두 활동이 아니라 하나의 폐쇄형 측정 체계(Closed Measurement Discipline)를 형성한다. 핵심성과지표는 어떤 증거를 수집해야 하는지를 결정하고, 계측(Instrumentation)은 해당 증거를 제공하며, 데이터 파이프라인은 이를 재현 가능한 엔지니어링 결론으로 변환한다. 이러한 체계는 현장 시험 방법론(Field-Testing Methodology)에서 이후 수행되는 자율이동로봇(AMR), 사족보행 로봇, 휴머노이드 및 무인항공기(UAV)의 현장 평가와 후속 데이터 기록 및 분석 활동을 위한 정량적 기반을 제공한다.

##  

## 05.04. AMR Field Test Navigation Safety Endurance

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

An AMR field test should determine whether the robot can navigate safely, consistently, and for sustained periods under conditions representative of its intended deployment. The campaign extends laboratory and simulation validation into real traffic environments containing changing obstacles, people, intersections, narrow passages, variable floor conditions, and communication disturbances. Navigation, safety, and endurance should be evaluated together because failures in one area can directly affect the others.

The test environment should represent the AMR operational design domain as closely as practical. Routes may include straight corridors, sharp turns, intersections, doorways, ramps, docking stations, elevators, loading areas, reflective surfaces, and regions with limited clearance. Environmental conditions such as illumination, floor friction, dust, pedestrian density, wireless coverage, and temporary obstacles should be documented so results can be associated with specific operating conditions.

Before dynamic testing begins, the AMR configuration should be recorded and verified. Software release, navigation stack parameters, localization map, safety-controller configuration, sensor calibration, payload, battery condition, maximum speed, acceleration limits, and network settings should be preserved with the trial metadata. Changes during the campaign must be tracked because even small parameter modifications can significantly alter navigation behavior or stopping performance.

Navigation testing should begin with repeatable point-to-point missions under controlled conditions. The robot can be commanded between predefined start and goal poses while position estimates, planned paths, executed trajectories, velocities, replanning events, and completion times are recorded. Core measures include mission success rate, path deviation, localization error, travel time, path efficiency, goal-position accuracy, and the frequency of operator intervention or autonomous recovery.

Localization performance should be evaluated across conditions that challenge the sensing and mapping system. Repetitive corridors, glass surfaces, sparse geometric features, moving crowds, temporary layout changes, low illumination, and wheel slip can degrade localization. External reference measurements or surveyed landmarks should be used where appropriate to distinguish true pose error from uncertainty reported internally by the localization algorithm.

Obstacle avoidance testing should include both static and dynamic objects. Static obstacles can verify detection, path replanning, clearance, and deadlock recovery, while moving pedestrians, carts, forklifts, or controlled robotic targets can evaluate prediction and responsive avoidance. The test should measure minimum separation distance, speed adaptation, avoidance trajectory quality, stop behavior, replanning latency, and whether the robot resumes its mission safely after the interaction.

Intersection and blind-corner scenarios are important because the AMR may encounter objects that become visible only shortly before crossing its path. Trials should vary approach speed, crossing direction, obstacle velocity, and visibility where safe to do so. Evaluation should focus on detection timing, deceleration behavior, protective responses, clearance, and recovery rather than simply determining whether a collision occurred.

Navigation robustness should also be tested under controlled degradation. Examples include temporary path blockage, localization uncertainty, intermittent sensor observations, reduced wireless quality, unavailable route segments, or delayed mission updates. The objective is to determine whether the robot can replan, stop safely, request assistance, or transition into an appropriate degraded state instead of continuing with invalid assumptions.

Safety testing should verify the protective functions that constrain AMR motion independently of normal navigation behavior. Safety scanners, bumpers, emergency stops, protective fields, speed limits, direction-dependent safety zones, and safety-controller interfaces should be exercised according to the approved protocol. The test should confirm that protective actions occur predictably and that normal autonomous software cannot bypass required safety constraints.

Stopping performance should be evaluated at representative speeds, payloads, floor conditions, and approach geometries. Engineers should measure the sequence from hazard detection through safety logic activation and commanded deceleration to the final stationary state. Stopping time and distance should be analyzed with synchronized timestamps because sensor latency, communication delay, controller response, actuator dynamics, tire behavior, and payload mass can all influence the result.

Human-proximity testing requires particularly conservative procedures. Controlled scenarios can evaluate how the AMR responds to pedestrians approaching from the front, side, rear, intersections, or occluded regions. The purpose is to verify detection, speed reduction, protective stopping, separation maintenance, and safe restart behavior. Personnel should never be used as uncontrolled collision targets; test procedures must preserve independent protective measures and clear abort authority.

Emergency-stop testing should confirm both the physical response and the system-state transition. Activation should bring the AMR into the defined safe state, inhibit unintended motion, generate the expected diagnostic or safety event, and require the prescribed reset procedure before operation resumes. Tests should also confirm that releasing the emergency-stop device alone does not cause unexpected automatic motion when an explicit restart authorization is required.

Payload variation can significantly affect AMR behavior and should therefore be included in representative field trials. Empty, nominal, and maximum authorized payload conditions may change acceleration, braking distance, traction, energy consumption, suspension behavior, and localization performance. Payload position and center-of-mass changes should also be considered when they are relevant to the mechanical configuration or intended logistics application.

Endurance testing evaluates whether acceptable navigation and safety performance can be sustained over extended operation rather than demonstrated for a few successful missions. The AMR should execute repeated representative routes and tasks for a defined duration, mission count, distance, or battery cycle while telemetry is collected continuously. The workload should approximate real deployment patterns, including motion, waiting, docking, charging, communication, and task transitions.

Long-duration testing should monitor gradual degradation as well as explicit failures. Battery state of charge, voltage, current, motor temperature, compute temperature, CPU and GPU utilization, memory consumption, storage usage, network quality, localization confidence, sensor health, and software process status can reveal developing problems. Trends are important because memory leaks, thermal throttling, calibration drift, and communication instability may emerge only after many hours.

Charging and docking behavior should be included when autonomous charging is part of normal AMR operation. Testing should evaluate docking success rate, alignment accuracy, retry behavior, charging initiation, communication with charging infrastructure, departure after charging, and recovery from unsuccessful docking attempts. Repeated charge-and-resume cycles can expose integration problems that are not visible when endurance testing is performed with manual battery management.

Traffic interaction should be tested when multiple robots or industrial vehicles share the operating environment. Relevant scenarios include corridor contention, intersection conflicts, blocked goals, queue formation, overtaking restrictions, and fleet-management rerouting. Measurements should capture mission delay, deadlock frequency, waiting time, traffic recovery, communication events, and whether safety behavior remains correct when multiple moving agents influence local planning simultaneously.

Failure recovery is a major component of endurance evaluation. The campaign should record localization loss, navigation deadlock, planner failure, sensor dropout, communication interruption, software restart, charging failure, and other operational anomalies. Each event should be classified according to whether the AMR recovered autonomously, required remote assistance, required physical intervention, or could not continue the mission.

Operator intervention should be treated as a measurable outcome rather than hidden from the success statistics. Every intervention should record its reason, duration, type, and resulting robot state. Mission results should distinguish fully autonomous completion from assisted completion. Metrics such as interventions per kilometer, per mission, or per operating hour provide a useful indication of whether nominal navigation performance can translate into practical autonomous deployment.

Field data should combine navigation logs, safety-controller events, sensor data, actuator telemetry, synchronized video, external observations, network measurements, and environmental metadata. Standardized event timestamps make it possible to reconstruct sequences involving detection, planning, control, safety intervention, and physical motion. Data completeness should be verified after important trials so that unusual behavior can be analyzed rather than remaining an unexplained observation.

Results should be analyzed by scenario and operating condition rather than only as global averages. A high overall mission success rate may conceal repeated failures at narrow doors, reflective corridors, crowded intersections, docking stations, or low-friction surfaces. Percentiles, failure distributions, intervention rates, safety events, and condition-specific results provide a more realistic characterization of deployment readiness than a single aggregate score.

Completion criteria for an AMR field campaign should combine navigation performance, safety compliance, endurance, and recoverability. Successful deployment readiness requires more than reaching goals without collision; the robot must maintain acceptable localization, respond correctly to hazards, preserve safety constraints, tolerate representative disturbances, operate for sustained periods, and recover predictably from foreseeable failures without excessive human assistance.

The resulting field evidence should remain traceable to the tested configuration, environment, trial protocol, raw logs, KPI calculations, anomalies, and acceptance decisions. This creates a reproducible basis for regression testing, reliability improvement, incident investigation, and subsequent certification activities. Within the field-testing methodology, AMR testing therefore demonstrates how environment setup, instrumentation, and KPI definition are integrated into platform-specific validation.

자율이동로봇(AMR) 현장 시험은 로봇이 의도된 배치 환경을 대표하는 조건에서 안전하고 일관되며 장시간 지속적으로 내비게이션을 수행할 수 있는지를 검증해야 한다. 시험 캠페인은 실험실 및 시뮬레이션 검증을 변화하는 장애물, 사람, 교차로, 좁은 통로, 다양한 바닥 조건 및 통신 장애가 존재하는 실제 교통 환경으로 확장한다. 내비게이션(Navigation), 안전성(Safety), 내구성(Endurance)은 한 영역의 문제가 다른 영역에 직접 영향을 줄 수 있으므로 통합적으로 평가해야 한다.

시험 환경은 가능한 범위에서 자율이동로봇의 운용 설계 영역(Operational Design Domain)을 충실하게 대표해야 한다. 시험 경로에는 직선 복도, 급회전 구간, 교차로, 출입문, 경사로, 도킹 스테이션(Docking Station), 엘리베이터, 적재 구역, 반사 표면 및 제한된 여유 공간이 포함될 수 있다. 조도, 바닥 마찰력, 먼지, 보행자 밀도, 무선 통신 커버리지 및 임시 장애물과 같은 환경 조건을 기록하여 시험 결과를 특정 운용 조건과 연결할 수 있어야 한다.

동적 시험(Dynamic Testing)을 시작하기 전에 자율이동로봇의 구성을 기록하고 검증해야 한다. 소프트웨어 릴리스, 내비게이션 스택(Navigation Stack) 매개변수, 위치추정 지도, 안전 제어기 구성, 센서 보정, 탑재물(Payload), 배터리 상태, 최대 속도, 가속도 제한 및 네트워크 설정을 시험 메타데이터와 함께 보존해야 한다. 작은 매개변수 변경도 내비게이션 동작이나 정지 성능에 상당한 영향을 줄 수 있으므로 캠페인 중 발생한 변경 사항을 추적해야 한다.

내비게이션 시험은 통제된 조건에서 반복 가능한 지점 간 임무(Point-to-Point Mission)부터 시작해야 한다. 로봇이 사전에 정의된 시작 자세와 목표 자세 사이를 이동하는 동안 위치 추정값, 계획 경로, 실제 실행 궤적, 속도, 재계획 이벤트 및 완료 시간을 기록할 수 있다. 핵심 측정값에는 임무 성공률, 경로 편차, 위치추정 오차, 이동 시간, 경로 효율성, 목표 위치 정확도 및 운영자 개입이나 자율 복구의 발생 빈도가 포함된다.

위치추정 성능(Localization Performance)은 센싱 및 지도 시스템에 어려움을 주는 다양한 조건에서 평가해야 한다. 반복적인 형태의 복도, 유리 표면, 기하학적 특징이 부족한 공간, 이동하는 군중, 일시적인 배치 변경, 낮은 조도 및 휠 슬립(Wheel Slip)은 위치추정 성능을 저하시킬 수 있다. 필요한 경우 외부 기준 측정 시스템이나 측량된 랜드마크를 사용하여 실제 위치 오차와 위치추정 알고리즘이 내부적으로 보고하는 불확실성을 구분해야 한다.

장애물 회피 시험(Obstacle Avoidance Testing)은 정적 물체와 동적 물체를 모두 포함해야 한다. 정적 장애물은 탐지, 경로 재계획, 안전거리 확보 및 교착상태 복구를 검증하는 데 사용할 수 있으며, 이동하는 보행자, 카트, 지게차 또는 통제된 로봇 표적은 예측 및 반응형 회피 성능을 평가하는 데 사용할 수 있다. 시험에서는 최소 이격 거리, 속도 조정, 회피 궤적 품질, 정지 동작, 재계획 지연시간 및 상호작용 이후 로봇이 안전하게 임무를 재개하는지를 측정해야 한다.

교차로와 사각지대 코너(Blind Corner) 시나리오는 자율이동로봇의 이동 경로를 가로지르기 직전에야 물체가 보일 수 있으므로 중요하다. 안전하게 수행할 수 있는 범위에서 접근 속도, 횡단 방향, 장애물 속도 및 가시성을 변화시키며 시험해야 한다. 평가는 단순히 충돌 발생 여부만 확인하는 것이 아니라 탐지 시점, 감속 동작, 보호 대응, 이격 거리 및 복구 동작을 중심으로 수행해야 한다.

내비게이션 강건성(Navigation Robustness)은 통제된 성능 저하 조건에서도 시험해야 한다. 일시적인 경로 차단, 위치추정 불확실성, 간헐적인 센서 관측, 무선 통신 품질 저하, 사용할 수 없는 경로 구간 또는 지연된 임무 업데이트 등이 대표적인 조건이다. 시험의 목적은 로봇이 잘못된 가정을 유지한 채 계속 운행하는 대신 경로를 재계획하거나, 안전하게 정지하거나, 지원을 요청하거나, 적절한 성능 저하 상태(Degraded State)로 전환할 수 있는지를 확인하는 것이다.

안전 시험(Safety Testing)은 정상적인 내비게이션 동작과 독립적으로 자율이동로봇의 움직임을 제한하는 보호 기능(Protective Function)을 검증해야 한다. 안전 스캐너(Safety Scanner), 범퍼, 비상 정지(Emergency Stop), 보호 영역(Protective Field), 속도 제한, 이동 방향별 안전 구역 및 안전 제어기 인터페이스를 승인된 시험 프로토콜에 따라 시험해야 한다. 보호 동작이 예측 가능한 방식으로 발생하며 정상 자율주행 소프트웨어가 필수 안전 제약조건을 우회할 수 없음을 확인해야 한다.

정지 성능(Stopping Performance)은 대표적인 속도, 탑재물, 바닥 상태 및 접근 형상에서 평가해야 한다. 엔지니어는 위험요소 감지에서 안전 로직 활성화, 감속 명령, 최종 정지 상태에 이르는 전체 과정을 측정해야 한다. 센서 지연시간, 통신 지연, 제어기 응답, 액추에이터 동역학, 타이어 특성 및 탑재물 질량이 결과에 영향을 줄 수 있으므로 동기화된 타임스탬프를 사용하여 정지 시간과 정지 거리를 분석해야 한다.

사람 근접 시험(Human-Proximity Testing)은 특히 보수적인 절차를 적용해야 한다. 통제된 시나리오를 통해 사람이 로봇의 전방, 측면, 후방, 교차로 또는 가려진 영역에서 접근할 때 자율이동로봇이 어떻게 대응하는지 평가할 수 있다. 목적은 사람 탐지, 속도 감소, 보호 정지, 안전거리 유지 및 안전한 재출발 동작을 검증하는 것이다. 사람을 통제되지 않은 충돌 표적으로 사용해서는 안 되며 독립적인 보호 수단과 명확한 시험 중단 권한을 유지해야 한다.

비상 정지 시험(Emergency-Stop Testing)은 물리적인 정지 응답뿐만 아니라 시스템 상태 전이(System-State Transition)도 검증해야 한다. 비상 정지가 활성화되면 자율이동로봇이 정의된 안전 상태로 전환되고, 의도하지 않은 움직임이 억제되며, 예상된 진단 또는 안전 이벤트가 생성되고, 운용을 재개하기 전에 규정된 재설정 절차가 수행되어야 한다. 명시적인 재시작 승인이 필요한 시스템에서는 비상 정지 장치를 해제하는 것만으로 로봇이 자동으로 움직이지 않는지도 확인해야 한다.

탑재물 변화(Payload Variation)는 자율이동로봇의 동작에 상당한 영향을 줄 수 있으므로 대표적인 현장 시험에 포함해야 한다. 무부하, 정격 부하 및 최대 허용 부하 조건은 가속도, 제동 거리, 견인력, 에너지 소비, 서스펜션 동작 및 위치추정 성능을 변화시킬 수 있다. 기계적 구성이나 물류 응용에 영향을 주는 경우 탑재물의 위치와 무게중심(Center of Mass) 변화도 함께 고려해야 한다.

내구성 시험(Endurance Testing)은 몇 번의 성공적인 임무를 시연하는 수준을 넘어 허용 가능한 내비게이션 및 안전 성능을 장시간 유지할 수 있는지를 평가한다. 자율이동로봇은 정의된 운용 시간, 임무 횟수, 이동 거리 또는 배터리 주기 동안 대표적인 경로와 작업을 반복적으로 수행해야 하며, 전체 과정에서 텔레메트리를 지속적으로 수집해야 한다. 작업 부하는 이동, 대기, 도킹, 충전, 통신 및 작업 전환을 포함하여 실제 배치 환경의 운용 패턴과 유사해야 한다.

장시간 시험(Long-Duration Testing)은 명시적인 장애뿐만 아니라 점진적인 성능 저하도 모니터링해야 한다. 배터리 충전 상태(State of Charge), 전압, 전류, 모터 온도, 컴퓨팅 장치 온도, 중앙처리장치(CPU) 및 그래픽처리장치(GPU) 사용률, 메모리 소비량, 저장장치 사용량, 네트워크 품질, 위치추정 신뢰도, 센서 상태 및 소프트웨어 프로세스 상태 등을 통해 잠재적인 문제를 파악할 수 있다. 메모리 누수, 열 스로틀링(Thermal Throttling), 보정 드리프트 및 통신 불안정성은 수시간 운용 이후에만 나타날 수 있으므로 장기적인 추세 분석이 중요하다.

자율 충전(Autonomous Charging)이 정상적인 자율이동로봇 운용의 일부라면 충전 및 도킹 동작도 시험에 포함해야 한다. 도킹 성공률, 정렬 정확도, 재시도 동작, 충전 시작, 충전 인프라와의 통신, 충전 이후 출발 및 실패한 도킹 시도의 복구 동작을 평가해야 한다. 충전과 임무 재개를 반복하는 주기 시험은 수동 배터리 관리 방식의 내구성 시험에서는 발견하기 어려운 시스템 통합 문제를 드러낼 수 있다.

여러 로봇이나 산업용 차량이 동일한 운용 환경을 공유한다면 교통 상호작용(Traffic Interaction)을 시험해야 한다. 관련 시나리오에는 복도 점유 경쟁, 교차로 충돌 가능 상황, 차단된 목표 지점, 대기열 형성, 추월 제한 및 플릿 관리 시스템(Fleet Management System)의 경로 재설정 등이 포함된다. 임무 지연, 교착상태 빈도, 대기 시간, 교통 흐름 복구, 통신 이벤트 및 여러 이동 객체가 동시에 지역 경로 계획에 영향을 줄 때 안전 동작이 올바르게 유지되는지를 측정해야 한다.

장애 복구(Failure Recovery)는 내구성 평가의 주요 구성 요소이다. 시험 캠페인은 위치추정 손실, 내비게이션 교착상태, 플래너 장애, 센서 데이터 손실, 통신 중단, 소프트웨어 재시작, 충전 실패 및 기타 운용 이상 현상을 기록해야 한다. 각 이벤트는 자율이동로봇이 자율적으로 복구했는지, 원격 지원이 필요했는지, 물리적인 사람의 개입이 필요했는지 또는 임무를 계속할 수 없었는지에 따라 분류해야 한다.

운영자 개입(Operator Intervention)은 성공 통계에서 숨기는 것이 아니라 측정 가능한 시험 결과로 취급해야 한다. 모든 개입은 원인, 지속시간, 유형 및 개입 이후의 로봇 상태를 기록해야 한다. 임무 결과는 완전 자율 완료(Fully Autonomous Completion)와 지원을 통한 완료(Assisted Completion)를 구분해야 한다. 킬로미터당, 임무당 또는 운용 시간당 개입 횟수와 같은 지표는 정상적인 내비게이션 성능이 실제 자율 배치로 연결될 수 있는지를 평가하는 데 유용하다.

현장 데이터(Field Data)는 내비게이션 로그, 안전 제어기 이벤트, 센서 데이터, 액추에이터 텔레메트리, 동기화된 영상, 외부 관찰 데이터, 네트워크 측정값 및 환경 메타데이터를 결합해야 한다. 표준화된 이벤트 타임스탬프를 사용하면 탐지, 계획, 제어, 안전 개입 및 실제 물리적 움직임으로 이어지는 일련의 과정을 재구성할 수 있다. 중요한 시험 이후에는 데이터 완전성을 확인하여 비정상적인 동작이 원인을 알 수 없는 관찰 결과로 남지 않고 실제 분석으로 이어지도록 해야 한다.

시험 결과는 전체 평균만으로 평가하지 않고 시나리오 및 운용 조건별로 분석해야 한다. 전체 임무 성공률이 높더라도 좁은 출입문, 반사 표면이 있는 복도, 혼잡한 교차로, 도킹 스테이션 또는 마찰력이 낮은 표면에서 반복적으로 장애가 발생할 수 있다. 백분위수(Percentile), 장애 분포, 운영자 개입률, 안전 이벤트 및 조건별 결과는 하나의 종합 점수보다 실제 배치 준비도(Deployment Readiness)를 더욱 현실적으로 보여준다.

자율이동로봇 현장 시험 캠페인의 완료 기준(Completion Criteria)은 내비게이션 성능, 안전 규정 준수, 내구성 및 복구 가능성(Recoverability)을 통합해야 한다. 실제 배치 준비 상태는 단순히 충돌 없이 목표 지점에 도달하는 것만으로 판단할 수 없다. 로봇은 허용 가능한 위치추정 성능을 유지하고, 위험요소에 올바르게 대응하며, 안전 제약조건을 유지하고, 대표적인 장애 조건을 견디며, 장시간 운용되고, 과도한 사람의 지원 없이 예측 가능한 방식으로 예상 가능한 장애에서 복구할 수 있어야 한다.

최종 현장 시험 증거(Field Evidence)는 시험된 시스템 구성, 환경, 시험 프로토콜, 원시 로그(Raw Log), 핵심성과지표(KPI) 계산 결과, 이상 현상 및 승인 결정까지 추적할 수 있어야 한다. 이를 통해 회귀 시험(Regression Testing), 신뢰성 개선, 사고 조사 및 후속 인증 활동을 위한 재현 가능한 기반을 구축할 수 있다. 따라서 자율이동로봇 현장 시험은 환경 설정, 계측(Instrumentation), 핵심성과지표 정의가 플랫폼별 검증(Platform-Specific Validation)으로 통합되는 대표적인 현장 시험 방법론을 제공한다.

##  

## 05.05. Quadruped Field Test Terrain Gait Stability

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

Quadruped field testing evaluates whether a legged robot can maintain reliable locomotion across terrain conditions that represent its intended operational environment. Unlike wheeled platforms, a quadruped must continuously coordinate foothold selection, body motion, contact forces, balance, and terrain perception. Field validation therefore focuses on the interaction among terrain difficulty, gait behavior, stability, recovery capability, and sustained mechanical performance.

The test campaign should begin with a precisely documented robot configuration. Controller version, locomotion policy, gait parameters, perception model, state estimator, joint firmware, actuator limits, payload, battery state, foot design, and safety settings should be recorded for every trial. Configuration traceability is especially important for learning-based locomotion because relatively small policy or parameter changes can produce substantial differences in dynamic behavior.

Terrain should be treated as a controlled test variable rather than as an informal property of the field site. Representative conditions can include flat concrete, asphalt, grass, gravel, soil, sand, wet surfaces, slopes, stairs, curbs, rocks, loose material, and irregular natural terrain. Surface friction, compliance, roughness, inclination, obstacle dimensions, and terrain transitions should be characterized whenever they materially affect locomotion performance.

Testing should progress from predictable surfaces toward increasingly difficult terrain. Initial trials can establish baseline walking performance on level ground before introducing slopes, steps, discontinuities, low-friction regions, deformable surfaces, or irregular footholds. This progression allows engineers to identify the point at which locomotion quality begins to degrade while limiting unnecessary exposure of the robot and personnel to high-energy falls or uncontrolled motion.

Gait evaluation should examine how effectively the quadruped coordinates leg motion under different speeds and terrain conditions. Walking, trotting, crawling, pacing, or platform-specific locomotion modes may require separate evaluation. Relevant measurements include commanded and achieved velocity, stride frequency, step length, stance and swing duration, duty factor, foot placement error, contact timing, and the consistency of gait cycles across repeated trials.

Gait-transition testing is important when the robot changes speed, terrain, direction, or locomotion mode during operation. Transitions should be evaluated for discontinuities in body velocity, excessive joint motion, foot slip, unexpected contact, or temporary instability. A successful transition should preserve controllability and body stability rather than merely complete the switch between gait states without triggering a fall.

Stability evaluation should characterize the robot\'s ability to control body pose and momentum while maintaining suitable ground contacts. Roll, pitch, yaw, body height, angular velocity, acceleration, joint states, foot contact patterns, and estimated contact forces can be monitored throughout each trial. Large oscillations, repeated corrective stepping, excessive body attitude error, or unstable contact switching may indicate deteriorating stability before an actual fall occurs.

Foot-ground interaction provides critical evidence about locomotion quality. Instrumentation should identify expected and unexpected contacts, foot slip, impact intensity, contact duration, and loss of support. External video and terrain references can supplement onboard estimates because contact state estimation may itself become unreliable on loose, deformable, wet, or highly irregular surfaces where accurate foothold information is most important.

Slope testing should include ascending, descending, and traversing across inclines where these conditions belong to the intended operating domain. Tests can gradually increase inclination while monitoring tracking error, body attitude, foot slip, actuator loading, and recovery behavior. Descending slopes may require separate attention because braking, impact, and forward momentum can create different stability limitations from those observed during ascent.

Stair and step testing should characterize both perception and physical locomotion capability. Step height, depth, edge geometry, approach angle, speed, and visibility influence successful traversal. The robot should demonstrate appropriate foothold placement, body clearance, contact sequencing, and recovery when a planned foothold is unavailable. Testing should include approach and departure behavior because failures frequently occur during terrain transitions rather than at the center of the obstacle.

Irregular terrain testing should evaluate adaptation to surfaces where footholds cannot be assumed to lie on a common plane. Rocks, blocks, uneven ground, or controlled stepping structures can expose limitations in terrain perception, local planning, state estimation, and whole-body control. Performance should be assessed using traversal success, speed, foot-placement accuracy, slip frequency, body-motion variation, intervention rate, and terrain-specific failure modes.

External disturbances can be introduced under carefully controlled safety conditions to evaluate recovery capability. Moderate pushes, unexpected compliant surfaces, small foothold displacement, or controlled contact disturbances can test whether the robot can redistribute support, modify foot placement, or execute recovery steps. Disturbance magnitude should be measurable and increased progressively so recovery boundaries can be characterized without turning the trial into an uncontrolled destructive test.

Slip and trip recovery deserve separate evaluation because they represent common real-world disturbances. A slipping stance foot can rapidly alter support forces, while an unexpected swing-foot collision can disrupt the planned gait cycle. Engineers should examine detection latency, corrective joint response, compensatory stepping, body attitude recovery, and whether the robot returns to nominal locomotion without operator assistance.

Fall behavior must be considered even when the primary objective is preventing falls. The test plan should define conditions requiring an immediate abort, safe shutdown behavior, operator exclusion zones, fall containment, and post-fall inspection procedures. A robot that detects unrecoverable instability should transition toward the safest achievable state rather than continuing aggressive control actions that increase risk to hardware or nearby personnel.

Terrain perception should be evaluated together with locomotion when the robot uses cameras, LiDAR, depth sensors, or learned perception to select footholds and trajectories. Lighting variation, vegetation, reflective surfaces, shadows, dust, water, and visually ambiguous terrain can affect estimated geometry. Field tests should correlate perception errors with downstream foothold decisions so failures are not incorrectly attributed only to the locomotion controller.

State-estimation robustness is equally important because dynamic legged locomotion depends on accurate estimates of body motion and contact state. IMU drift, joint measurement error, foot slip, vibration, visual degradation, or temporary loss of external localization can affect control. Trials should determine whether estimation uncertainty remains bounded and whether the robot responds safely when confidence in its state or terrain representation decreases.

Payload testing should examine how additional mass and changes in center of gravity affect locomotion. Representative payload configurations can influence joint torque, body attitude, foot loading, energy consumption, gait timing, and recovery margins. Tests should include payload placement as well as mass because asymmetric or elevated loads can introduce stability challenges that are not represented by a centrally mounted test weight.

Endurance trials should repeat representative terrain and gait sequences for sufficient duration to reveal degradation that short demonstrations cannot expose. Joint temperature, motor current, battery state, compute utilization, actuator faults, foot wear, structural loosening, localization quality, and gait metrics should be monitored over time. Performance trends can reveal thermal limits, mechanical wear, calibration drift, or policy degradation before a complete locomotion failure occurs.

Energy efficiency should be evaluated alongside locomotion performance because terrain and gait selection can significantly alter power consumption. Energy per unit distance, energy per mission, battery discharge rate, actuator power, and locomotion speed can be compared across surfaces and gait modes. A gait that achieves high speed but produces excessive thermal loading or energy consumption may be unsuitable for sustained field deployment.

Operator intervention should be recorded as a formal performance outcome. Manual stabilization, remote command correction, gait-mode override, emergency stopping, physical recovery, or robot repositioning should be timestamped and classified. Trials completed with assistance should not be reported as equivalent to fully autonomous traversal, because intervention frequency provides an important measure of practical deployment readiness.

Field data should synchronize joint states, actuator commands, IMU measurements, contact estimates, perception outputs, terrain maps, localization, battery and thermal telemetry, safety events, and external video. Where available, external motion tracking or surveyed terrain geometry can provide independent references. Accurate synchronization allows engineers to reconstruct the chain from terrain perception through control decisions to physical contact and body response.

Results should be stratified by terrain class, slope, gait, speed, payload, environmental condition, and disturbance level rather than reduced to a single success rate. Percentile body-motion errors, slip frequency, fall rate, recovery success, intervention frequency, energy consumption, and traversal time can expose different operational limits. Failure cases should be preserved because they define the practical boundary of the validated locomotion envelope.

A quadruped should be considered field-ready only when it demonstrates repeatable traversal, stable gait behavior, controlled terrain adaptation, predictable disturbance recovery, and acceptable endurance throughout the intended operating domain. Field validation therefore connects terrain, gait, stability, perception, state estimation, energy, and recovery into a unified assessment of locomotion capability, consistent with the platform-specific field-testing structure of the testing methodology.

사족보행 로봇(Quadruped) 현장 시험은 다족 로봇(Legged Robot)이 의도된 운용 환경을 대표하는 다양한 지형 조건에서 신뢰할 수 있는 이동 성능을 유지할 수 있는지를 평가한다. 바퀴형 플랫폼과 달리 사족보행 로봇은 발 디딤 위치(Foothold), 몸체 움직임, 접촉력(Contact Force), 균형 및 지형 인지를 지속적으로 조정해야 한다. 따라서 현장 검증(Field Validation)은 지형 난이도, 보행 동작(Gait Behavior), 안정성, 복구 능력 및 지속적인 기계적 성능 사이의 상호작용을 중심으로 수행해야 한다.

시험 캠페인은 정확하게 문서화된 로봇 구성(Robot Configuration)에서 시작해야 한다. 제어기 버전, 이동 정책(Locomotion Policy), 보행 매개변수, 인지 모델, 상태 추정기(State Estimator), 관절 펌웨어, 액추에이터 제한, 탑재물(Payload), 배터리 상태, 발 구조 및 안전 설정을 모든 시험에서 기록해야 한다. 특히 학습 기반 이동(Learning-Based Locomotion)은 작은 정책이나 매개변수 변경도 동적 동작에 상당한 차이를 만들 수 있으므로 구성 추적성(Configuration Traceability)이 중요하다.

지형(Terrain)은 현장 시험 장소의 비공식적인 특성이 아니라 통제된 시험 변수(Test Variable)로 취급해야 한다. 대표적인 조건에는 평탄한 콘크리트, 아스팔트, 잔디, 자갈, 흙, 모래, 젖은 표면, 경사면, 계단, 연석, 암석, 느슨한 지면 및 불규칙한 자연 지형 등이 포함될 수 있다. 표면 마찰력, 탄성, 거칠기, 경사도, 장애물 치수 및 지형 전환 조건이 이동 성능에 실질적인 영향을 주는 경우 이를 특성화해야 한다.

시험은 예측 가능한 표면에서 시작하여 점차 난도가 높은 지형으로 진행해야 한다. 초기 시험에서는 평탄한 지면에서 기본 보행 성능을 확인한 후 경사면, 단차, 불연속 지형, 저마찰 영역, 변형 가능한 표면 또는 불규칙한 발 디딤 영역을 단계적으로 추가할 수 있다. 이러한 진행 방식은 로봇과 시험 인력이 고에너지 낙상이나 통제되지 않은 움직임에 불필요하게 노출되는 것을 제한하면서 이동 품질이 저하되기 시작하는 지점을 파악할 수 있게 한다.

보행 평가(Gait Evaluation)는 서로 다른 속도와 지형 조건에서 사족보행 로봇이 다리 움직임을 얼마나 효과적으로 조정하는지를 평가해야 한다. 걷기(Walking), 트로팅(Trotting), 크롤링(Crawling), 페이싱(Pacing) 또는 플랫폼별 이동 모드를 각각 평가할 수 있다. 관련 측정값에는 명령 속도와 실제 속도, 보폭 주파수, 보폭 길이, 입각기와 유각기 지속시간, 듀티 팩터(Duty Factor), 발 디딤 위치 오차, 접촉 타이밍 및 반복 시험에서의 보행 주기 일관성이 포함된다.

보행 전환 시험(Gait-Transition Testing)은 로봇이 운용 중 속도, 지형, 이동 방향 또는 보행 모드를 변경할 때 중요하다. 전환 과정에서 몸체 속도의 불연속성, 과도한 관절 움직임, 발 미끄러짐, 예상하지 못한 접촉 또는 일시적인 불안정성이 발생하는지를 평가해야 한다. 성공적인 전환은 단순히 낙상 없이 보행 상태를 변경하는 것이 아니라 제어 가능성과 몸체 안정성을 유지해야 한다.

안정성 평가(Stability Evaluation)는 적절한 지면 접촉을 유지하면서 로봇이 몸체 자세와 운동량을 제어할 수 있는 능력을 특성화해야 한다. 각 시험에서 롤(Roll), 피치(Pitch), 요(Yaw), 몸체 높이, 각속도, 가속도, 관절 상태, 발 접촉 패턴 및 추정 접촉력을 모니터링할 수 있다. 큰 진동, 반복적인 보정 스텝, 과도한 몸체 자세 오차 또는 불안정한 접촉 전환은 실제 낙상이 발생하기 전에 안정성이 저하되고 있음을 나타낼 수 있다.

발과 지면의 상호작용(Foot-Ground Interaction)은 이동 품질을 평가하는 핵심적인 증거를 제공한다. 계측 시스템(Instrumentation)은 예상된 접촉과 예상하지 못한 접촉, 발 미끄러짐, 충격 강도, 접촉 지속시간 및 지지력 손실을 식별할 수 있어야 한다. 느슨하거나 변형 가능하거나 젖어 있거나 매우 불규칙한 표면에서는 접촉 상태 추정 자체가 불안정해질 수 있으므로 외부 영상과 지형 기준 정보를 사용하여 온보드 추정값을 보완할 수 있다.

경사면 시험(Slope Testing)은 해당 조건이 의도된 운용 영역에 포함되는 경우 오르막, 내리막 및 경사면 횡단을 모두 포함해야 한다. 경사도를 점진적으로 증가시키면서 추종 오차, 몸체 자세, 발 미끄러짐, 액추에이터 부하 및 복구 동작을 모니터링할 수 있다. 내리막에서는 제동, 충격 및 전방 운동량이 오르막과 다른 안정성 한계를 만들 수 있으므로 별도의 평가가 필요할 수 있다.

계단 및 단차 시험(Stair and Step Testing)은 인지 능력과 물리적인 이동 능력을 함께 평가해야 한다. 단차 높이와 깊이, 모서리 형상, 접근 각도, 속도 및 가시성은 성공적인 통과 여부에 영향을 준다. 로봇은 적절한 발 디딤 위치, 몸체 여유 공간, 접촉 순서 및 계획된 발 디딤 위치를 사용할 수 없을 때의 복구 능력을 보여야 한다. 장애물 중심부보다 지형 전환 구간에서 장애가 빈번하게 발생할 수 있으므로 접근과 이탈 동작도 시험해야 한다.

불규칙 지형 시험(Irregular Terrain Testing)은 발 디딤 위치가 하나의 평면에 존재한다고 가정할 수 없는 표면에 대한 적응 능력을 평가해야 한다. 암석, 블록, 고르지 않은 지면 또는 통제된 디딤 구조물은 지형 인지, 지역 경로 계획(Local Planning), 상태 추정 및 전신 제어(Whole-Body Control)의 한계를 드러낼 수 있다. 통과 성공률, 이동 속도, 발 디딤 정확도, 미끄러짐 빈도, 몸체 움직임 변화, 개입률 및 지형별 장애 유형을 이용하여 성능을 평가해야 한다.

외부 교란(External Disturbance)은 복구 능력을 평가하기 위해 신중하게 통제된 안전 조건에서 적용할 수 있다. 적당한 밀기, 예상하지 못한 탄성 표면, 작은 발 디딤 위치 변화 또는 통제된 접촉 교란을 통해 로봇이 지지력을 재분배하고 발 위치를 수정하거나 복구 스텝(Recovery Step)을 수행할 수 있는지를 평가할 수 있다. 교란의 크기는 측정 가능해야 하며 시험이 통제되지 않은 파괴 시험으로 변하지 않도록 점진적으로 증가시켜 복구 한계를 파악해야 한다.

미끄러짐 및 걸림 복구(Slip and Trip Recovery)는 실제 환경에서 흔하게 발생할 수 있는 교란이므로 별도로 평가해야 한다. 입각 상태의 발이 미끄러지면 지지력이 급격히 변할 수 있으며, 유각 상태의 발이 예상하지 못한 물체와 충돌하면 계획된 보행 주기가 깨질 수 있다. 엔지니어는 탐지 지연시간, 관절의 보정 응답, 보상 스텝(Compensatory Stepping), 몸체 자세 복구 및 운영자 지원 없이 정상적인 이동 상태로 복귀할 수 있는지를 평가해야 한다.

낙상 동작(Fall Behavior)은 낙상을 방지하는 것이 주요 목표인 경우에도 반드시 고려해야 한다. 시험 계획은 즉각적인 시험 중단이 필요한 조건, 안전 종료(Safe Shutdown) 동작, 운영자 출입 제한 구역, 낙상 보호 수단 및 낙상 이후 점검 절차를 정의해야 한다. 로봇이 복구할 수 없는 불안정성을 감지한 경우 하드웨어 또는 주변 인력에 대한 위험을 증가시키는 공격적인 제어를 계속하기보다 가능한 가장 안전한 상태로 전환해야 한다.

로봇이 카메라, 라이다(LiDAR), 깊이 센서 또는 학습 기반 인지(Learned Perception)를 이용하여 발 디딤 위치와 이동 궤적을 결정한다면 지형 인지(Terrain Perception)를 이동 성능과 함께 평가해야 한다. 조명 변화, 식생, 반사 표면, 그림자, 먼지, 물 및 시각적으로 모호한 지형은 추정된 지형 형상에 영향을 줄 수 있다. 현장 시험에서는 인지 오류와 이후의 발 디딤 결정 사이의 관계를 분석하여 장애 원인을 단순히 이동 제어기의 문제로 잘못 판단하지 않도록 해야 한다.

동적 다족보행(Dynamic Legged Locomotion)은 몸체 움직임과 접촉 상태에 대한 정확한 추정에 의존하므로 상태 추정 강건성(State-Estimation Robustness)도 중요하다. 관성측정장치(IMU) 드리프트, 관절 측정 오차, 발 미끄러짐, 진동, 시각 정보 저하 또는 외부 위치추정의 일시적인 손실은 제어 성능에 영향을 줄 수 있다. 시험에서는 추정 불확실성이 제한된 범위에서 유지되는지와 로봇이 자신의 상태 또는 지형 표현에 대한 신뢰도가 감소할 때 안전하게 대응하는지를 확인해야 한다.

탑재물 시험(Payload Testing)은 추가 질량과 무게중심(Center of Gravity)의 변화가 이동 성능에 미치는 영향을 평가해야 한다. 대표적인 탑재물 구성은 관절 토크, 몸체 자세, 발 하중, 에너지 소비, 보행 타이밍 및 복구 여유도에 영향을 줄 수 있다. 비대칭 또는 높은 위치에 배치된 하중은 중앙에 배치된 시험용 무게만으로는 나타나지 않는 안정성 문제를 유발할 수 있으므로 탑재물의 질량뿐만 아니라 배치 위치도 시험해야 한다.

내구성 시험(Endurance Trial)은 짧은 시연으로는 발견하기 어려운 성능 저하를 확인할 수 있도록 대표적인 지형과 보행 순서를 충분한 시간 동안 반복해야 한다. 관절 온도, 모터 전류, 배터리 상태, 컴퓨팅 자원 사용률, 액추에이터 장애, 발 마모, 구조적 풀림, 위치추정 품질 및 보행 지표를 시간에 따라 모니터링해야 한다. 성능 추세를 분석하면 완전한 이동 장애가 발생하기 전에 열적 한계, 기계적 마모, 보정 드리프트 또는 정책 성능 저하를 파악할 수 있다.

지형과 보행 선택은 전력 소비에 상당한 영향을 줄 수 있으므로 에너지 효율(Energy Efficiency)을 이동 성능과 함께 평가해야 한다. 단위 거리당 에너지, 임무당 에너지, 배터리 방전율, 액추에이터 전력 및 이동 속도를 표면과 보행 모드별로 비교할 수 있다. 높은 속도를 달성하는 보행이라도 과도한 열 부하 또는 에너지 소비를 발생시킨다면 장시간 현장 배치에는 적합하지 않을 수 있다.

운영자 개입(Operator Intervention)은 공식적인 성능 결과로 기록해야 한다. 수동 안정화, 원격 명령 수정, 보행 모드 강제 변경, 비상 정지, 물리적 복구 또는 로봇 재배치 등을 타임스탬프와 함께 기록하고 분류해야 한다. 지원을 받아 완료된 시험은 완전 자율 통과(Fully Autonomous Traversal)와 동일하게 보고해서는 안 되며, 개입 빈도는 실제 배치 준비도(Deployment Readiness)를 평가하는 중요한 지표가 된다.

현장 데이터(Field Data)는 관절 상태, 액추에이터 명령, 관성측정장치 측정값, 접촉 추정값, 인지 출력, 지형 지도, 위치추정, 배터리 및 열 텔레메트리, 안전 이벤트 및 외부 영상을 시간 동기화하여 수집해야 한다. 가능한 경우 외부 동작 추적(External Motion Tracking) 또는 측량된 지형 형상을 독립적인 기준으로 사용할 수 있다. 정확한 시간 동기화를 통해 지형 인지에서 제어 의사결정, 실제 접촉 및 몸체 응답으로 이어지는 전체 과정을 재구성할 수 있다.

시험 결과는 하나의 성공률로 축소하지 않고 지형 유형, 경사도, 보행 방식, 속도, 탑재물, 환경 조건 및 교란 수준에 따라 계층화하여 분석해야 한다. 몸체 움직임 오차의 백분위수(Percentile), 미끄러짐 빈도, 낙상률, 복구 성공률, 개입 빈도, 에너지 소비 및 통과 시간을 통해 서로 다른 운용 한계를 파악할 수 있다. 장애 사례는 검증된 이동 영역(Validated Locomotion Envelope)의 실질적인 경계를 정의하므로 반드시 보존해야 한다.

사족보행 로봇은 의도된 운용 영역 전체에서 반복 가능한 지형 통과, 안정적인 보행 동작, 통제된 지형 적응, 예측 가능한 교란 복구 및 허용 가능한 내구성을 입증했을 때 현장 운용 준비(Field-Ready)가 되었다고 판단할 수 있다. 따라서 현장 검증은 지형, 보행, 안정성, 인지, 상태 추정, 에너지 및 복구 능력을 하나의 통합된 이동 능력 평가(Unified Locomotion Assessment)로 연결하여 사족보행 로봇의 실제 환경 운용 가능성을 검증한다.

##  

## 05.06. Humanoid Field Test Task Execution HRI

![](images/image6.png){width="7.268055555555556in" height="7.268055555555556in"}

Humanoid field testing evaluates whether a robot can execute complete physical tasks safely and reliably while interacting with people and human-designed environments. Unlike isolated locomotion or manipulation tests, field evaluation combines perception, balance, navigation, whole-body control, manipulation, task reasoning, communication, and safety. The objective is to determine whether these capabilities remain coordinated during realistic, extended task execution.

The campaign should begin with a controlled configuration baseline. Hardware revision, joint firmware, controller parameters, perception models, task policy, VLA or generalist policy version, safety configuration, payload, end-effector setup, battery state, and software release should be recorded. Humanoid behavior can change significantly when one subsystem is updated, so every field result must remain traceable to the exact integrated system configuration.

Field environments should represent spaces designed primarily for humans rather than simplified robot test cells. Relevant conditions may include doors, tables, shelves, chairs, stairs, narrow passages, workstations, tools, containers, uneven floors, and moving people. Object locations, workspace geometry, illumination, surface properties, pedestrian activity, and environmental changes should be documented because they influence both task execution and human-robot interaction.

Task execution should be evaluated as an end-to-end process rather than as a collection of independently successful motions. A representative task may require receiving an instruction, identifying relevant objects, navigating to a workspace, positioning the body, grasping an object, manipulating it, transporting it, placing it correctly, and confirming completion. Failure at any stage can prevent successful completion even when individual capabilities perform well in isolation.

Task success criteria should distinguish complete autonomous execution from partial or assisted completion. The test protocol should define the initial state, goal state, permitted actions, timeout, acceptable object placement, safety constraints, and conditions requiring intervention. Metrics can include task success rate, completion time, number of retries, planning failures, manipulation errors, operator interventions, recovery success, and the fraction of subtasks completed without assistance.

Long-horizon tasks deserve special attention because errors can accumulate across sequential actions. Small localization errors, imperfect grasps, object displacement, misunderstood instructions, or state-estimation drift may become significant after many task steps. Field trials should therefore include multi-stage activities that require the humanoid to preserve task context, update its understanding of the environment, and recover when intermediate results differ from the expected state.

Whole-body coordination should be evaluated whenever manipulation and locomotion occur within the same task. Reaching toward distant objects, carrying loads, opening doors, pushing carts, bending, turning, or transferring objects can alter balance and support requirements. Measurements should capture body posture, joint states, center-of-mass behavior, contact conditions, hand forces, task progress, and recovery actions so manipulation success is not evaluated independently of physical stability.

Manipulation trials should represent realistic object diversity. Objects can vary in size, shape, mass, compliance, surface friction, handle geometry, visual appearance, and placement. The robot should be evaluated not only on successful grasp acquisition but also on maintaining grasp stability, avoiding excessive force, detecting failed grasps, repositioning when necessary, and placing or handing over objects without creating unsafe conditions.

Bimanual tasks can expose integration problems that are less visible in single-arm manipulation. Carrying large objects, opening containers, stabilizing an item while manipulating it, or transferring an object between hands requires coordinated force, pose, and timing control. Field testing should examine synchronization between arms, whole-body compensation, object stability, collision avoidance, and recovery when one hand loses or fails to establish the expected contact.

Human-robot interaction should be evaluated as an integral part of humanoid operation rather than as a separate user-interface feature. Humans may provide spoken instructions, gestures, objects, corrections, or confirmation while sharing the robot\'s workspace. Tests should determine whether the humanoid correctly perceives relevant human actions, interprets commands, maintains appropriate spatial behavior, and communicates its intentions or limitations sufficiently for predictable collaboration.

Instruction-following tests should include variation in wording, order, context, and task complexity when language-driven control is part of the system. The robot should connect an instruction to the physical environment, identify the intended entities, select appropriate actions, and recognize when the instruction cannot be executed safely or unambiguously. Incorrect confident execution can be more hazardous than requesting clarification or refusing an unsupported action.

Object handover provides a useful combined test of perception, manipulation, timing, and human interaction. The humanoid must identify the recipient, approach an appropriate transfer pose, present the object safely, detect when the person has established control, and release at the correct time. Evaluation can consider handover success, interaction time, excessive force, dropped objects, premature release, failed transfer detection, and the need for human adaptation.

Human proximity introduces safety requirements beyond task completion. Tests should examine behavior when a person enters the workspace, crosses the robot\'s path, approaches during manipulation, or unexpectedly changes position. The humanoid should respond through appropriate speed reduction, motion modification, protective stopping, or task suspension. Safety evaluation should consider the robot\'s entire body because arms, hands, torso, legs, carried objects, and loss of balance can all create hazards.

Contact-rich interaction requires careful force monitoring. Tasks involving handovers, collaborative carrying, guided motion, or incidental contact should verify that force and torque remain within defined operational limits and that unexpected contact is detected promptly. The robot should transition to an appropriate response when contact differs from the expected interaction instead of continuing a high-force trajectory based on an outdated task assumption.

Social and behavioral predictability can influence operational safety even when formal safety functions remain intact. Sudden arm motion, unexplained pauses, unexpected approach trajectories, or ambiguous task transitions can cause nearby people to react unpredictably. Field observations should therefore capture whether robot motion and communication provide sufficient cues for people to understand what the humanoid is doing and what action is expected from them.

Recovery behavior should be evaluated intentionally because realistic humanoid tasks rarely proceed exactly as planned. Test scenarios can include displaced objects, unavailable targets, failed grasps, blocked paths, dropped items, misunderstood instructions, temporary perception loss, or interrupted human interaction. The robot should detect the changed state, reassess the task, retry within permitted limits, request assistance, or terminate safely rather than repeatedly executing an invalid plan.

Balance and fall risk must remain monitored throughout task execution. Manipulation, payload changes, external contact, stepping, reaching, and unexpected human interaction can shift the robot toward its stability limits. Field testing should record balance-related events, corrective stepping, support changes, excessive body attitude, instability detection, and protective responses. Fall zones and emergency procedures should remain active whenever a full-size humanoid is operating near personnel.

Operator intervention should be explicitly recorded and classified. Remote corrections, task replanning assistance, manual object repositioning, locomotion overrides, emergency stops, physical stabilization, and recovery after falls represent different levels of assistance. A task completed after substantial intervention should not be counted as equivalent to autonomous success. Intervention frequency and duration are important indicators of practical humanoid autonomy.

Repeated trials should include controlled variations rather than reproducing only one favorable arrangement. Object positions, human positions, instruction phrasing, approach direction, lighting, clutter, and task sequence can be varied within the intended operating domain. This helps determine whether successful behavior represents robust task competence or memorization of a narrow configuration and provides evidence about generalization across realistic field conditions.

Endurance evaluation should extend beyond locomotion to repeated whole-body task cycles. Continuous reaching, walking, grasping, carrying, interaction, and computation can expose actuator heating, battery depletion, mechanical wear, perception degradation, memory growth, thermal throttling, or policy instability. Task success, intervention rate, cycle time, joint temperature, energy consumption, and system health should be monitored for trends over prolonged operation.

Field instrumentation should synchronize perception outputs, language or task commands, policy decisions, navigation states, joint trajectories, force and torque measurements, safety events, operator actions, and external video. This allows investigators to reconstruct the relationship between what the humanoid perceived, what it inferred, what action it selected, and what physically occurred. Such traceability is essential for diagnosing complex failures spanning multiple subsystems.

Results should be analyzed by task type, environment, object class, interaction mode, human proximity, autonomy level, and operating duration. A single overall success rate can conceal important weaknesses, such as reliable navigation but poor handover behavior or strong manipulation with frequent human assistance. Failure distributions, recovery success, intervention frequency, safety events, completion time, and task-specific success provide a more meaningful assessment.

A humanoid should be considered ready for broader field operation only when it demonstrates repeatable end-to-end task execution, stable whole-body behavior, reliable human interaction, predictable recovery, and acceptable safety over representative conditions. Within the field-testing methodology, humanoid evaluation therefore integrates task execution and HRI with perception, locomotion, manipulation, safety, instrumentation, and measurable operational evidence.

휴머노이드(Humanoid) 현장 시험은 로봇이 사람 및 인간 중심으로 설계된 환경과 상호작용하면서 완전한 물리적 작업을 안전하고 신뢰성 있게 수행할 수 있는지를 평가한다. 개별적인 이동이나 조작 시험과 달리 현장 평가는 인지(Perception), 균형, 내비게이션(Navigation), 전신 제어(Whole-Body Control), 조작(Manipulation), 작업 추론(Task Reasoning), 의사소통 및 안전성을 통합한다. 목표는 실제적인 장시간 작업 수행 중에도 이러한 기능들이 서로 조화롭게 유지되는지를 확인하는 것이다.

시험 캠페인은 통제된 구성 기준선(Configuration Baseline)에서 시작해야 한다. 하드웨어 개정 버전, 관절 펌웨어, 제어기 매개변수, 인지 모델, 작업 정책(Task Policy), 비전-언어-행동(VLA) 또는 범용 정책(Generalist Policy) 버전, 안전 구성, 탑재물(Payload), 엔드 이펙터(End-Effector) 구성, 배터리 상태 및 소프트웨어 릴리스를 기록해야 한다. 하나의 하위 시스템 변경만으로도 휴머노이드 동작이 크게 달라질 수 있으므로 모든 현장 시험 결과는 정확한 통합 시스템 구성까지 추적할 수 있어야 한다.

현장 환경(Field Environment)은 단순화된 로봇 시험 셀이 아니라 기본적으로 사람을 위해 설계된 공간을 대표해야 한다. 관련 조건에는 문, 테이블, 선반, 의자, 계단, 좁은 통로, 작업대, 도구, 용기, 고르지 않은 바닥 및 이동하는 사람이 포함될 수 있다. 물체 위치, 작업 공간 형상, 조명, 표면 특성, 보행자 활동 및 환경 변화를 기록해야 하며, 이러한 요소는 작업 수행과 인간-로봇 상호작용(HRI)에 모두 영향을 준다.

작업 수행(Task Execution)은 독립적으로 성공한 여러 동작의 집합이 아니라 종단간 과정(End-to-End Process)으로 평가해야 한다. 대표적인 작업은 명령 수신, 관련 물체 식별, 작업 공간으로의 이동, 몸체 위치 정렬, 물체 파지, 조작, 운반, 정확한 위치에 배치 및 완료 확인을 요구할 수 있다. 개별 기능이 독립적으로 우수하게 작동하더라도 어느 한 단계에서 장애가 발생하면 전체 작업을 성공적으로 완료하지 못할 수 있다.

작업 성공 기준(Task Success Criteria)은 완전 자율 수행과 부분적 또는 지원을 받은 완료를 구분해야 한다. 시험 프로토콜은 초기 상태, 목표 상태, 허용된 행동, 시간 제한, 허용 가능한 물체 배치, 안전 제약조건 및 개입이 필요한 조건을 정의해야 한다. 측정 지표에는 작업 성공률, 완료 시간, 재시도 횟수, 계획 실패, 조작 오류, 운영자 개입, 복구 성공률 및 도움 없이 완료한 하위 작업의 비율 등이 포함될 수 있다.

장기 순차 작업(Long-Horizon Task)은 연속적인 행동 과정에서 오류가 누적될 수 있으므로 특별한 평가가 필요하다. 작은 위치추정 오차, 불완전한 파지, 물체 위치 변화, 잘못 이해한 명령 또는 상태 추정 드리프트(State-Estimation Drift)는 많은 작업 단계가 진행된 이후 상당한 문제로 발전할 수 있다. 따라서 현장 시험에는 휴머노이드가 작업 맥락을 유지하고 환경에 대한 이해를 갱신하며 중간 결과가 예상 상태와 달라졌을 때 복구할 수 있는 다단계 활동을 포함해야 한다.

조작과 이동이 동일한 작업에서 수행되는 경우 전신 협응(Whole-Body Coordination)을 평가해야 한다. 멀리 있는 물체에 손을 뻗거나, 물체를 운반하거나, 문을 열거나, 카트를 밀거나, 몸을 숙이거나, 회전하거나, 물체를 전달하는 동작은 균형과 지지 조건을 변화시킬 수 있다. 몸체 자세, 관절 상태, 무게중심(Center of Mass) 동작, 접촉 조건, 손의 힘, 작업 진행 상태 및 복구 동작을 측정하여 조작 성공 여부를 물리적 안정성과 분리해서 평가하지 않도록 해야 한다.

조작 시험(Manipulation Trial)은 실제 환경에서 나타나는 다양한 물체를 대표해야 한다. 물체는 크기, 형상, 질량, 유연성, 표면 마찰력, 손잡이 형상, 시각적 외관 및 배치 상태가 서로 다를 수 있다. 로봇은 단순히 성공적으로 물체를 파지하는 능력뿐만 아니라 파지 안정성을 유지하고, 과도한 힘을 방지하고, 실패한 파지를 감지하고, 필요한 경우 위치를 재조정하며, 위험한 상황을 만들지 않고 물체를 배치하거나 전달할 수 있는지를 평가해야 한다.

양손 작업(Bimanual Task)은 단일 팔 조작에서는 쉽게 드러나지 않는 시스템 통합 문제를 나타낼 수 있다. 큰 물체 운반, 용기 열기, 물체를 고정하면서 조작하기 또는 한 손에서 다른 손으로 물체를 전달하는 작업은 힘, 자세 및 타이밍의 협응을 요구한다. 현장 시험에서는 양팔 사이의 동기화, 전신 보상(Whole-Body Compensation), 물체 안정성, 충돌 회피 및 한쪽 손이 예상한 접촉을 잃거나 접촉 형성에 실패했을 때의 복구 능력을 평가해야 한다.

인간-로봇 상호작용(Human-Robot Interaction)은 별도의 사용자 인터페이스 기능이 아니라 휴머노이드 운용의 통합된 일부로 평가해야 한다. 사람은 로봇과 작업 공간을 공유하면서 음성 명령, 제스처, 물체, 수정 지시 또는 확인 정보를 제공할 수 있다. 시험에서는 휴머노이드가 관련된 사람의 행동을 정확하게 인지하고, 명령을 해석하며, 적절한 공간적 행동을 유지하고, 예측 가능한 협업이 가능하도록 자신의 의도나 한계를 충분히 전달하는지를 확인해야 한다.

언어 기반 제어(Language-Driven Control)가 시스템의 일부라면 명령 수행 시험(Instruction-Following Test)은 표현 방식, 순서, 맥락 및 작업 복잡성의 변화를 포함해야 한다. 로봇은 명령을 물리적 환경과 연결하고, 의도된 대상 객체를 식별하고, 적절한 행동을 선택하며, 명령을 안전하게 수행할 수 없거나 의미가 불명확한 경우 이를 인식해야 한다. 잘못된 명령을 확신을 가지고 실행하는 것은 추가 설명을 요청하거나 지원되지 않는 행동의 수행을 거부하는 것보다 더 위험할 수 있다.

물체 전달(Object Handover)은 인지, 조작, 타이밍 및 인간 상호작용을 통합적으로 평가할 수 있는 유용한 시험이다. 휴머노이드는 물체를 받을 사람을 식별하고, 적절한 전달 자세로 접근하며, 물체를 안전하게 제시하고, 상대방이 물체를 확실히 잡았는지를 감지한 후 적절한 시점에 물체를 놓아야 한다. 전달 성공률, 상호작용 시간, 과도한 힘, 물체 낙하, 조기 해제, 전달 실패 감지 및 사람이 로봇에 맞추어 행동해야 하는 정도 등을 평가할 수 있다.

사람 근접(Human Proximity)은 단순한 작업 완료 이상의 안전 요구사항을 발생시킨다. 시험에서는 사람이 작업 공간에 진입하거나, 로봇의 이동 경로를 가로지르거나, 조작 작업 중 접근하거나, 예상하지 못하게 위치를 변경할 때 로봇의 행동을 평가해야 한다. 휴머노이드는 적절한 속도 감소, 동작 수정, 보호 정지(Protective Stop) 또는 작업 일시 중단을 수행해야 한다. 팔, 손, 몸통, 다리, 운반 물체 및 균형 상실 모두 위험을 발생시킬 수 있으므로 로봇의 전신을 대상으로 안전성을 평가해야 한다.

접촉이 많은 상호작용(Contact-Rich Interaction)에서는 힘을 신중하게 모니터링해야 한다. 물체 전달, 협력 운반, 유도 동작 또는 우발적 접촉이 포함된 작업에서는 힘과 토크가 정의된 운용 한계 내에서 유지되고 예상하지 못한 접촉이 신속하게 감지되는지를 검증해야 한다. 접촉 상태가 예상된 상호작용과 달라진 경우 로봇은 오래된 작업 가정에 기반하여 높은 힘의 궤적을 계속 실행하지 않고 적절한 대응 상태로 전환해야 한다.

사회적 및 행동적 예측 가능성(Social and Behavioral Predictability)은 공식적인 안전 기능이 정상적으로 유지되더라도 운용 안전에 영향을 줄 수 있다. 갑작스러운 팔 움직임, 이유를 알 수 없는 정지, 예상하지 못한 접근 궤적 또는 모호한 작업 전환은 주변 사람의 예측하지 못한 반응을 유발할 수 있다. 따라서 현장 관찰에서는 로봇의 움직임과 의사소통이 사람이 휴머노이드의 현재 행동과 자신에게 기대되는 행동을 이해할 수 있을 만큼 충분한 단서를 제공하는지를 평가해야 한다.

복구 동작(Recovery Behavior)은 실제 휴머노이드 작업이 항상 계획대로 진행되는 것은 아니므로 의도적으로 평가해야 한다. 시험 시나리오에는 위치가 변경된 물체, 사용할 수 없는 목표물, 파지 실패, 차단된 경로, 떨어뜨린 물체, 잘못 이해한 명령, 일시적인 인지 손실 또는 중단된 인간 상호작용 등이 포함될 수 있다. 로봇은 변경된 상태를 감지하고 작업을 다시 평가하며, 허용된 범위에서 재시도하거나, 지원을 요청하거나, 잘못된 계획을 반복적으로 실행하지 않고 안전하게 작업을 종료해야 한다.

균형과 낙상 위험(Fall Risk)은 작업 수행 전체 과정에서 지속적으로 모니터링해야 한다. 조작, 탑재물 변화, 외부 접촉, 보행, 손 뻗기 및 예상하지 못한 인간 상호작용은 로봇을 안정성 한계에 접근시킬 수 있다. 현장 시험에서는 균형 관련 이벤트, 보정 스텝(Corrective Stepping), 지지 상태 변화, 과도한 몸체 자세, 불안정성 감지 및 보호 대응을 기록해야 한다. 실물 크기의 휴머노이드가 사람 근처에서 작동하는 동안에는 낙상 구역(Fall Zone)과 비상 대응 절차를 항상 유지해야 한다.

운영자 개입(Operator Intervention)은 명확하게 기록하고 분류해야 한다. 원격 수정, 작업 재계획 지원, 수동 물체 재배치, 이동 명령 강제 변경, 비상 정지, 물리적 안정화 및 낙상 이후 복구는 서로 다른 수준의 지원을 의미한다. 상당한 사람의 개입 이후 완료된 작업을 완전 자율 성공과 동일하게 평가해서는 안 된다. 개입 빈도와 지속시간은 휴머노이드의 실질적인 자율성(Practical Humanoid Autonomy)을 평가하는 중요한 지표이다.

반복 시험(Repeated Trial)은 하나의 유리한 배치만 반복하는 것이 아니라 통제된 조건 변화를 포함해야 한다. 물체 위치, 사람 위치, 명령 표현, 접근 방향, 조명, 주변 복잡도 및 작업 순서를 의도된 운용 영역 내에서 변화시킬 수 있다. 이를 통해 성공적인 행동이 좁은 특정 구성의 암기에 의한 것인지 실제로 강건한 작업 수행 능력(Robust Task Competence)을 의미하는지를 판단하고 현실적인 현장 조건에 대한 일반화(Generalization) 능력을 평가할 수 있다.

내구성 평가(Endurance Evaluation)는 단순한 이동을 넘어 반복적인 전신 작업 주기(Whole-Body Task Cycle)를 대상으로 수행해야 한다. 지속적인 손 뻗기, 보행, 파지, 운반, 상호작용 및 연산은 액추에이터 발열, 배터리 소모, 기계적 마모, 인지 성능 저하, 메모리 사용량 증가, 열 스로틀링(Thermal Throttling) 또는 정책 불안정성을 발생시킬 수 있다. 장시간 운용 동안 작업 성공률, 개입률, 작업 주기 시간, 관절 온도, 에너지 소비 및 시스템 상태의 변화 추세를 모니터링해야 한다.

현장 계측(Field Instrumentation)은 인지 출력, 언어 또는 작업 명령, 정책 의사결정, 내비게이션 상태, 관절 궤적, 힘과 토크 측정값, 안전 이벤트, 운영자 행동 및 외부 영상을 시간 동기화하여 수집해야 한다. 이를 통해 휴머노이드가 무엇을 인지했고, 어떻게 추론했으며, 어떤 행동을 선택했고, 실제 물리적 환경에서 어떤 결과가 발생했는지를 연결하여 재구성할 수 있다. 이러한 추적성(Traceability)은 여러 하위 시스템에 걸쳐 발생하는 복잡한 장애를 진단하는 데 필수적이다.

시험 결과는 작업 유형, 환경, 물체 종류, 상호작용 방식, 사람과의 근접 정도, 자율성 수준 및 운용 시간에 따라 분석해야 한다. 하나의 전체 성공률만 사용하면 내비게이션은 신뢰할 수 있지만 물체 전달 성능이 낮거나, 조작 성능은 우수하지만 사람의 개입이 빈번한 것과 같은 중요한 약점을 감출 수 있다. 장애 분포, 복구 성공률, 개입 빈도, 안전 이벤트, 완료 시간 및 작업별 성공률을 함께 분석해야 보다 의미 있는 평가가 가능하다.

휴머노이드는 대표적인 운용 조건에서 반복 가능한 종단간 작업 수행, 안정적인 전신 동작, 신뢰할 수 있는 인간 상호작용, 예측 가능한 복구 및 허용 가능한 안전성을 입증한 경우에만 더 광범위한 현장 운용에 준비되었다고 판단해야 한다. 따라서 현장 시험 방법론(Field-Testing Methodology)에서 휴머노이드 평가는 작업 수행과 인간-로봇 상호작용을 인지, 이동, 조작, 안전, 계측 및 측정 가능한 운용 증거와 통합하여 실제 환경에서의 종합적인 시스템 능력을 검증하는 과정이다.

##  

## 05.07. UAV Flight Test Campaign Protocol

![](images/image7.png){width="7.268055555555556in" height="7.268055555555556in"}

A UAV flight test campaign is a structured progression of ground and airborne evaluations used to demonstrate that the aircraft, flight software, autonomy functions, payload, communication links, and safety mechanisms operate correctly within a defined flight envelope. Unlike routine demonstrations, each flight should be treated as a controlled engineering experiment with explicit objectives, configuration records, measurable acceptance criteria, and predefined termination conditions.

Campaign planning should define the aircraft configuration, mission profile, test airspace, altitude and speed limits, payload condition, environmental constraints, personnel responsibilities, and required instrumentation. The protocol should also identify which capabilities are being evaluated during each flight. Navigation, flight control, perception, communication, autonomous mission execution, emergency functions, endurance, and payload operations should be separated when independent evidence is required.

Flight testing should follow an incremental build-up strategy. Ground checks and restrained tests should precede low-risk hover or short-flight evaluations, followed by progressively wider speed, altitude, maneuver, payload, and autonomy conditions. Each expansion should occur only after the preceding configuration has satisfied its acceptance criteria. This approach limits exposure to unknown behavior and creates evidence for controlled expansion of the validated flight envelope.

Configuration control is essential because flight behavior can change after modifications to software, firmware, controller gains, propulsion hardware, payload, sensors, or vehicle mass properties. Every test record should identify the flight software release, autonomy stack, parameter set, AI model version where applicable, airframe configuration, propulsion system, battery, payload mass, center of gravity, sensor calibration, communication settings, and relevant ground infrastructure.

A formal preflight procedure should verify aircraft readiness before propulsion is enabled. Structural condition, propellers or rotors, motors, batteries, power distribution, flight computer, navigation sensors, GNSS, IMU, altimeter, communication links, telemetry, payload interfaces, logging systems, and emergency functions should be checked. Any discrepancy affecting flightworthiness, safety, or required evidence should result in a no-go decision until the issue is resolved.

Environmental conditions should be treated as measurable test variables rather than background information. Wind speed and direction, gusts, temperature, precipitation, visibility, lighting, atmospheric conditions, and GNSS quality can influence flight behavior and perception. The protocol should establish permitted environmental limits for each test phase and record actual conditions so performance changes can be correlated with the environment during post-flight analysis.

The flight area should have clearly defined operational and containment boundaries. Launch and recovery zones, expected trajectories, altitude limits, exclusion areas, emergency landing locations, and personnel positions should be established before the test. Geofencing can provide an additional software boundary, but it should not replace procedural and physical risk controls. Flight termination criteria should address unintended boundary excursions or loss of containment confidence.

Initial airborne testing should establish basic controllability and state-estimation performance. Hover stability, altitude holding, attitude control, heading control, position holding, and low-speed translation can be evaluated before more demanding maneuvers are attempted. Relevant measurements include position error, attitude error, velocity tracking, oscillation, control effort, actuator saturation, vibration, and the frequency of unexpected mode transitions or operator intervention.

Trajectory-following tests should evaluate whether the UAV can accurately execute commanded paths across representative speeds and maneuver geometries. Straight segments, turns, climbs, descents, waypoint transitions, and approach trajectories can expose different controller and estimator limitations. Cross-track error, altitude error, speed error, waypoint accuracy, overshoot, settling behavior, and mission completion time provide quantitative measures of flight performance.

Autonomous navigation testing should examine the complete chain from sensing and localization through planning, guidance, and control. Where applicable, scenarios can include waypoint missions, obstacle avoidance, route replanning, landing-site selection, or operation with degraded positioning. Autonomous success should be distinguished from missions requiring pilot correction because intervention frequency is a critical indicator of practical autonomy.

Communication testing should evaluate both command-and-control and telemetry links throughout the intended operating region. Signal strength, latency, packet loss, link interruption, handover behavior, command acknowledgement, and recovery after temporary disconnection should be recorded. The aircraft should demonstrate predictable behavior when communication quality deteriorates, including continuation, holding, return, landing, or another predefined contingency response.

GNSS and navigation degradation should be evaluated only within carefully controlled test conditions. Temporary positioning degradation, reduced satellite visibility, inconsistent measurements, or transition to alternative localization can reveal dependencies that are hidden during ideal GNSS operation. The objective is to verify that navigation uncertainty is detected and that the aircraft enters an appropriate degraded or contingency state instead of continuing with unreliable position assumptions.

Safety-function testing should verify behaviors associated with communication loss, low battery, navigation failure, propulsion anomalies, geofence violation, excessive attitude, or other monitored hazards. Depending on the system design, responses may include hover, return-to-home, controlled descent, emergency landing, mission abort, or flight termination. The expected response and trigger threshold should be defined before the test rather than interpreted after an event occurs.

Return-to-home and emergency landing functions require dedicated evaluation because they may become the final protective layer after other failures. Tests should verify activation logic, route generation, altitude management, obstacle considerations, landing-zone approach, and final touchdown behavior. Recovery functions should also be tested from different positions and mission phases because a response that is safe near the launch site may not be appropriate throughout the entire operating area.

Payload testing should consider the influence of mass, center of gravity, aerodynamic effects, power consumption, and payload activity on flight performance. Representative empty, nominal, and maximum authorized configurations may require separate trials. For cargo UAVs, payload restraint, load distribution, release or transfer mechanisms, and changes in handling characteristics should be evaluated because payload configuration can alter stability, endurance, and emergency behavior.

Endurance testing should determine whether flight performance remains acceptable throughout realistic mission duration rather than only during short maneuvers. Battery voltage, current, state of charge, propulsion temperature, flight-computer temperature, compute utilization, navigation quality, communication status, and controller behavior should be monitored continuously. Reserve-energy requirements should be incorporated into termination criteria so endurance testing does not consume the safety margin required for recovery.

Repeated mission cycles can reveal degradation that a single long flight may not expose. Charging, battery replacement, payload loading, startup, navigation initialization, takeoff, mission execution, landing, shutdown, and data transfer can be repeated as an operational sequence. This allows engineers to evaluate dispatch reliability and identify intermittent faults, calibration problems, connector wear, initialization failures, or procedural weaknesses between flights.

Human roles must remain explicit throughout the campaign even when the aircraft operates autonomously. The test director, remote pilot, safety observer, payload operator, instrumentation personnel, and ground crew should understand their responsibilities and communication procedures. Authority to abort the flight must be unambiguous, and safety personnel should be able to prioritize containment and personnel protection over completion of the planned test objective.

Flight instrumentation should synchronize flight-controller states, IMU data, GNSS measurements, actuator commands, motor telemetry, battery data, navigation estimates, mission events, communication statistics, payload states, safety events, and ground observations. External tracking, surveyed references, radar, or synchronized video may provide independent evidence where required. Accurate timing enables reconstruction of fast event sequences that cannot be understood from isolated logs.

Post-flight inspection should occur before the aircraft is returned to service or reconfigured. Engineers should examine structural components, propulsion hardware, batteries, connectors, landing gear, payload attachments, and other critical elements for damage, loosening, overheating, or abnormal wear. Software logs and health reports should also be reviewed for faults that may not have been visible to the flight crew during operation.

Post-flight data review should determine whether the test produced valid evidence before the campaign proceeds to the next envelope point. Missing logs, synchronization failures, unexpected configuration changes, environmental excursions, or instrumentation faults can invalidate an otherwise successful flight. Anomalies should be classified and reviewed, and significant unexplained behavior should prevent further envelope expansion until the associated risk is understood.

Results should be analyzed by flight phase, maneuver, payload, environmental condition, autonomy mode, and vehicle configuration rather than reduced to a single mission success rate. Tracking error, intervention frequency, safety events, energy consumption, communication performance, recovery success, and anomaly distributions provide complementary evidence. Failed and aborted flights are particularly important because they identify boundaries of the validated operating envelope.

A UAV flight campaign is complete only when the required operating envelope has been covered with sufficient repeatability and the aircraft has demonstrated predictable nominal, degraded, and contingency behavior. The resulting evidence should remain traceable from objectives and configuration through flight records, telemetry, anomalies, KPI calculations, and acceptance decisions, providing a reproducible foundation for subsequent analysis, safety assessment, and certification-oriented field evidence.

무인항공기(UAV) 비행 시험 캠페인은 항공기, 비행 소프트웨어, 자율 기능, 탑재물(Payload), 통신 링크 및 안전 메커니즘이 정의된 비행 영역(Flight Envelope) 내에서 올바르게 작동하는지를 입증하기 위한 체계적인 지상 및 비행 평가 과정이다. 일반적인 시연과 달리 각 비행은 명확한 목표, 구성 기록, 측정 가능한 허용 기준 및 사전에 정의된 종료 조건을 갖춘 통제된 엔지니어링 실험(Engineering Experiment)으로 수행해야 한다.

시험 캠페인 계획(Campaign Planning)은 항공기 구성, 임무 프로파일(Mission Profile), 시험 공역, 고도 및 속도 제한, 탑재물 상태, 환경 제약조건, 인력별 책임 및 필요한 계측(Instrumentation)을 정의해야 한다. 또한 프로토콜은 각 비행에서 어떤 기능을 평가하는지 명확히 해야 한다. 독립적인 증거가 필요한 경우 내비게이션(Navigation), 비행 제어, 인지, 통신, 자율 임무 수행, 비상 기능, 내구성 및 탑재물 운용을 구분하여 평가해야 한다.

비행 시험은 점진적인 시험 영역 확장 전략(Incremental Build-Up Strategy)을 따라야 한다. 지상 점검과 구속 시험(Restrained Test)을 먼저 수행한 후 위험도가 낮은 호버링(Hover) 또는 단거리 비행 평가를 수행하고, 이후 속도, 고도, 기동, 탑재물 및 자율 운용 조건을 단계적으로 확대해야 한다. 각 확장은 이전 단계의 구성이 허용 기준을 충족한 경우에만 수행하여 알려지지 않은 동작에 대한 노출을 제한하고 검증된 비행 영역을 통제된 방식으로 확대할 수 있어야 한다.

소프트웨어, 펌웨어, 제어기 게인(Controller Gain), 추진 하드웨어, 탑재물, 센서 또는 항공기의 질량 특성이 변경되면 비행 동작도 달라질 수 있으므로 구성 관리(Configuration Control)가 필수적이다. 모든 시험 기록에는 비행 소프트웨어 릴리스, 자율비행 스택(Autonomy Stack), 매개변수 세트, 적용되는 경우 인공지능 모델(AI Model) 버전, 기체 구성, 추진 시스템, 배터리, 탑재물 질량, 무게중심(Center of Gravity), 센서 보정, 통신 설정 및 관련 지상 인프라를 기록해야 한다.

정식 비행 전 절차(Preflight Procedure)는 추진 시스템을 활성화하기 전에 항공기의 비행 준비 상태를 검증해야 한다. 구조 상태, 프로펠러 또는 로터, 모터, 배터리, 전력 분배, 비행 컴퓨터, 항법 센서, 위성항법시스템(GNSS), 관성측정장치(IMU), 고도계, 통신 링크, 텔레메트리(Telemetry), 탑재물 인터페이스, 기록 시스템 및 비상 기능을 점검해야 한다. 비행 적합성, 안전 또는 필수 증거 수집에 영향을 주는 이상이 발견되면 문제가 해결될 때까지 비행 불가(No-Go) 결정을 내려야 한다.

환경 조건(Environmental Conditions)은 단순한 배경 정보가 아니라 측정 가능한 시험 변수로 취급해야 한다. 풍속과 풍향, 돌풍, 온도, 강수, 가시성, 조명, 대기 상태 및 위성항법시스템 품질은 비행 동작과 인지 성능에 영향을 줄 수 있다. 프로토콜은 각 시험 단계에 허용되는 환경 한계를 정의하고 실제 조건을 기록하여 비행 이후 분석에서 성능 변화와 환경 조건 사이의 관계를 파악할 수 있도록 해야 한다.

비행 구역에는 명확하게 정의된 운용 및 격리 경계(Containment Boundary)가 있어야 한다. 이륙 및 회수 구역, 예상 비행 궤적, 고도 제한, 출입 제한 구역, 비상 착륙 위치 및 시험 인력의 위치를 비행 전에 설정해야 한다. 지오펜싱(Geofencing)은 추가적인 소프트웨어 경계를 제공할 수 있지만 절차적 및 물리적 위험 통제를 대체해서는 안 된다. 비행 종료 기준에는 의도하지 않은 경계 이탈이나 격리 상태에 대한 신뢰 상실도 포함해야 한다.

초기 비행 시험은 기본적인 조종 가능성(Controllability)과 상태 추정(State Estimation) 성능을 확인해야 한다. 보다 어려운 기동을 수행하기 전에 호버링 안정성, 고도 유지, 자세 제어, 방향 유지, 위치 유지 및 저속 이동을 평가할 수 있다. 관련 측정값에는 위치 오차, 자세 오차, 속도 추종 성능, 진동, 제어 입력, 액추에이터 포화(Actuator Saturation), 기체 진동 및 예상하지 못한 모드 전환이나 운영자 개입의 빈도가 포함된다.

궤적 추종 시험(Trajectory-Following Test)은 무인항공기가 대표적인 속도와 기동 형상에서 명령된 경로를 정확하게 수행할 수 있는지를 평가해야 한다. 직선 구간, 선회, 상승, 하강, 웨이포인트(Waypoint) 전환 및 접근 궤적은 서로 다른 제어기와 상태 추정기의 한계를 드러낼 수 있다. 횡방향 경로 오차(Cross-Track Error), 고도 오차, 속도 오차, 웨이포인트 정확도, 오버슈트(Overshoot), 안정화 동작 및 임무 완료 시간을 통해 비행 성능을 정량적으로 평가할 수 있다.

자율 내비게이션 시험(Autonomous Navigation Testing)은 센싱과 위치추정에서 경로 계획, 유도(Guidance), 제어로 이어지는 전체 과정을 평가해야 한다. 시스템 구성에 따라 웨이포인트 임무, 장애물 회피, 경로 재계획, 착륙 지점 선택 또는 위치 정보가 저하된 상태에서의 운용 등을 시험할 수 있다. 조종사의 수정이 필요한 임무와 완전 자율 성공을 구분해야 하며, 개입 빈도는 실제 자율성(Practical Autonomy)을 평가하는 중요한 지표이다.

통신 시험(Communication Testing)은 의도된 운용 영역 전체에서 명령 및 제어(Command and Control) 링크와 텔레메트리 링크를 모두 평가해야 한다. 신호 강도, 지연시간(Latency), 패킷 손실, 링크 중단, 핸드오버(Handover) 동작, 명령 확인 및 일시적인 연결 손실 이후 복구 상태를 기록해야 한다. 통신 품질이 저하될 경우 항공기는 임무 지속, 대기, 복귀, 착륙 또는 사전에 정의된 다른 비상 대응을 포함하여 예측 가능한 동작을 수행해야 한다.

위성항법시스템 및 항법 성능 저하(GNSS and Navigation Degradation)는 신중하게 통제된 시험 조건에서만 평가해야 한다. 일시적인 위치 정보 품질 저하, 위성 가시성 감소, 일관되지 않은 측정값 또는 대체 위치추정 방식으로의 전환을 통해 이상적인 위성항법 환경에서는 드러나지 않는 시스템 의존성을 확인할 수 있다. 목적은 항법 불확실성이 감지되고 신뢰할 수 없는 위치 정보를 기반으로 비행을 계속하지 않으며 적절한 성능 저하 또는 비상 상태(Contingency State)로 전환되는지를 검증하는 것이다.

안전 기능 시험(Safety-Function Testing)은 통신 손실, 배터리 부족, 항법 장애, 추진계 이상, 지오펜스 위반, 과도한 자세 변화 또는 기타 모니터링 대상 위험과 관련된 동작을 검증해야 한다. 시스템 설계에 따라 호버링, 자동 복귀(Return-to-Home), 제어된 하강, 비상 착륙, 임무 중단 또는 비행 종료 등의 대응을 수행할 수 있다. 예상 대응과 작동 임계값은 이벤트가 발생한 이후 해석하는 것이 아니라 시험 전에 정의해야 한다.

자동 복귀(Return-to-Home)와 비상 착륙(Emergency Landing)은 다른 장애 발생 이후 최종 보호 계층이 될 수 있으므로 별도의 평가가 필요하다. 시험에서는 기능 활성화 로직, 복귀 경로 생성, 고도 관리, 장애물 고려, 착륙 구역 접근 및 최종 착지 동작을 검증해야 한다. 또한 이륙 지점 근처에서는 안전한 대응이라도 전체 운용 영역에서 항상 적합한 것은 아닐 수 있으므로 다양한 위치와 임무 단계에서 복구 기능을 시험해야 한다.

탑재물 시험(Payload Testing)은 질량, 무게중심, 공기역학적 영향, 전력 소비 및 탑재물 작동이 비행 성능에 미치는 영향을 고려해야 한다. 무부하, 정격 부하 및 최대 허용 부하 구성을 각각 시험해야 할 수 있다. 화물 무인항공기(Cargo UAV)의 경우 탑재물 고정, 하중 분포, 화물 해제 또는 전달 메커니즘 및 조종 특성의 변화를 평가해야 하며, 탑재물 구성은 안정성, 항속시간 및 비상 동작을 변화시킬 수 있다.

내구성 시험(Endurance Testing)은 짧은 기동에서만 성능을 평가하는 것이 아니라 실제적인 임무 지속시간 전체에서 비행 성능이 허용 가능한 수준으로 유지되는지를 확인해야 한다. 배터리 전압, 전류, 충전 상태(State of Charge), 추진계 온도, 비행 컴퓨터 온도, 연산 자원 사용률, 항법 품질, 통신 상태 및 제어기 동작을 지속적으로 모니터링해야 한다. 내구성 시험으로 복구에 필요한 안전 여유까지 소비하지 않도록 예비 에너지(Reserve Energy) 요구사항을 종료 기준에 포함해야 한다.

반복적인 임무 주기(Repeated Mission Cycle)는 한 번의 장시간 비행에서는 발견되지 않는 성능 저하를 드러낼 수 있다. 충전, 배터리 교체, 화물 적재, 시스템 시작, 항법 초기화, 이륙, 임무 수행, 착륙, 시스템 종료 및 데이터 전송을 하나의 운용 순서로 반복할 수 있다. 이를 통해 출동 신뢰성(Dispatch Reliability)을 평가하고 비행 사이에 발생하는 간헐적 장애, 보정 문제, 커넥터 마모, 초기화 실패 또는 절차상의 취약점을 식별할 수 있다.

항공기가 자율적으로 운용되는 경우에도 시험 캠페인 전체에서 사람의 역할(Human Roles)을 명확하게 유지해야 한다. 시험 책임자, 원격 조종사(Remote Pilot), 안전 관찰자, 탑재물 운영자, 계측 담당자 및 지상 인력은 자신의 책임과 통신 절차를 이해해야 한다. 비행 중단 권한은 명확해야 하며, 안전 담당자는 계획된 시험 목표의 완료보다 비행 영역 유지와 인원 보호를 우선할 수 있어야 한다.

비행 계측(Flight Instrumentation)은 비행 제어기 상태, 관성측정장치 데이터, 위성항법시스템 측정값, 액추에이터 명령, 모터 텔레메트리, 배터리 데이터, 항법 추정값, 임무 이벤트, 통신 통계, 탑재물 상태, 안전 이벤트 및 지상 관측 데이터를 시간 동기화하여 수집해야 한다. 필요한 경우 외부 추적 시스템, 측량된 기준점, 레이더 또는 동기화된 영상을 독립적인 증거로 사용할 수 있다. 정확한 시간 동기화는 개별 로그만으로 이해하기 어려운 빠른 이벤트의 연속 과정을 재구성할 수 있게 한다.

비행 후 점검(Post-Flight Inspection)은 항공기를 다시 운용하거나 구성을 변경하기 전에 수행해야 한다. 엔지니어는 구조 부품, 추진 하드웨어, 배터리, 커넥터, 착륙 장치, 탑재물 고정부 및 기타 핵심 요소에서 손상, 풀림, 과열 또는 비정상적인 마모가 발생했는지를 확인해야 한다. 또한 비행 중 시험 인력이 직접 확인하지 못했을 수 있는 장애를 식별하기 위해 소프트웨어 로그와 시스템 상태 보고서를 검토해야 한다.

비행 후 데이터 검토(Post-Flight Data Review)를 통해 시험 캠페인이 다음 비행 영역으로 진행되기 전에 해당 비행이 유효한 증거를 생성했는지를 판단해야 한다. 로그 누락, 동기화 장애, 예상하지 못한 구성 변경, 환경 조건의 허용 범위 이탈 또는 계측 장애가 발생하면 비행 자체가 성공적이었더라도 시험 결과가 무효가 될 수 있다. 이상 현상(Anomaly)을 분류하고 검토하며, 설명되지 않은 중요한 동작이 존재하는 경우 관련 위험이 충분히 이해될 때까지 시험 영역 확장을 중단해야 한다.

시험 결과는 하나의 임무 성공률로 축소하지 않고 비행 단계, 기동 방식, 탑재물, 환경 조건, 자율 운용 모드 및 기체 구성에 따라 분석해야 한다. 추종 오차, 운영자 개입 빈도, 안전 이벤트, 에너지 소비, 통신 성능, 복구 성공률 및 이상 현상 분포는 상호 보완적인 증거를 제공한다. 특히 실패하거나 중단된 비행은 검증된 운용 영역(Validated Operating Envelope)의 경계를 식별하는 중요한 자료이므로 반드시 보존하고 분석해야 한다.

무인항공기 비행 시험 캠페인은 요구되는 운용 영역이 충분한 반복성을 가지고 검증되고 항공기가 정상 상태(Nominal State), 성능 저하 상태(Degraded State) 및 비상 상태(Contingency State)에서 예측 가능한 동작을 입증한 경우에만 완료된 것으로 판단해야 한다. 최종 증거는 시험 목표와 시스템 구성에서 비행 기록, 텔레메트리, 이상 현상, 핵심성과지표(KPI) 계산 및 승인 결정까지 추적 가능해야 하며, 이후 분석, 안전성 평가 및 인증 중심 현장 증거(Certification-Oriented Field Evidence)를 위한 재현 가능한 기반을 제공해야 한다.

##  

## 05.08. Field Test Data Logging and Analysis Pipeline [w/Code]

![](images/image8.png){width="7.268055555555556in" height="7.268055555555556in"}

Field-test data logging should transform physical robot operation into a complete and reproducible digital record. The pipeline must capture not only whether a mission succeeded, but also the sequence of perception, estimation, planning, control, safety, communication, and physical events that produced the result. Logging should therefore be designed from validation objectives and KPI requirements rather than added after field testing has already begun.

A field-data pipeline typically begins at heterogeneous data sources distributed across the robot and test environment. These may include cameras, LiDAR, radar, IMU, GNSS, joint encoders, motor controllers, safety devices, network monitors, environmental sensors, external ground-truth systems, operator consoles, and synchronized video. Software outputs such as localization, maps, trajectories, detections, policy actions, diagnostics, and mission states should be captured with relevant raw measurements.

Logging architecture should distinguish high-bandwidth sensor streams from lower-rate state, event, and diagnostic information. Raw images and point clouds may require dedicated storage paths, while control commands, poses, safety events, and system-health metrics can use structured message logs. The architecture should preserve relationships among these sources so engineers can reconstruct system behavior without relying on manually aligned files or incomplete operator notes.

Time synchronization is fundamental to meaningful analysis. Sensor acquisition, perception output, planner decisions, controller commands, actuator responses, safety events, and external observations may occur within milliseconds of one another. A common clock based on PTP, GNSS timing, hardware triggers, or another validated synchronization mechanism should therefore be used where required, and the expected timing accuracy should be documented with each test configuration.

Timestamp semantics must also be preserved because identical-looking timestamps can represent different stages of a data path. A camera frame may contain exposure time, driver reception time, middleware publication time, processing time, and storage time. Latency analysis should use the timestamp corresponding to the actual event being measured. Otherwise buffering, scheduling jitter, network delay, or processing queues can produce misleading conclusions about system response.

Before each field run, the logging system should verify that required channels are active and storage resources are sufficient. Checks can include sensor stream availability, expected message rates, clock synchronization, disk capacity, write throughput, network connectivity, metadata completeness, and external recorder status. A robot should not begin a critical validation trial when essential evidence cannot be captured reliably, even if the robot itself appears operational.

Data-rate planning is especially important for sensor-rich robotic systems. Multiple high-resolution cameras, dense LiDAR, radar, audio, diagnostic traces, and AI outputs can generate sustained data rates that exceed storage or network capability. Engineers should estimate nominal and peak throughput, reserve capacity for long trials, and test the recording system under representative load so dropped frames or blocked processes do not invalidate the campaign.

Logging must be designed to avoid significantly altering the behavior being measured. Compression, serialization, disk writes, network transfer, and diagnostic tracing consume compute, memory, bandwidth, and power. Excessive instrumentation can introduce latency or thermal loading that would not exist during normal deployment. Logging overhead should therefore be measured, bounded, and included in configuration records when it can influence performance.

Every trial should receive a unique identifier linking raw data to its experimental context. Metadata should include test campaign, scenario, robot identifier, hardware configuration, software release, AI model version, map, payload, operator, environmental conditions, start and end times, and protocol revision. Consistent metadata prevents datasets from becoming anonymous collections of files whose engineering meaning can no longer be reconstructed.

Event logging provides a compact semantic layer above continuous telemetry. Events such as mission start, goal reached, localization loss, obstacle detection, replanning, operator intervention, protective stop, emergency stop, recovery, task failure, and mission completion should use standardized definitions. These markers allow automated analysis tools to segment long recordings and calculate durations, frequencies, transitions, and outcome statistics consistently.

Operator observations should be integrated into the data pipeline rather than maintained only in separate informal notes. Test personnel may observe wheel slip, unusual vibration, unexpected human behavior, environmental changes, visual obstruction, abnormal sound, or physical contact that onboard diagnostics cannot identify. Timestamped annotations make these observations searchable and allow them to be correlated with robot telemetry and synchronized video during analysis.

Immediately after a test, an ingestion stage should verify that expected files and streams were recorded successfully. File integrity, duration, message counts, timestamps, metadata, video readability, and external reference data can be checked automatically. Detecting missing evidence while the test configuration remains available allows the trial to be repeated before equipment, weather, terrain, or software conditions change.

Raw data should normally be preserved as immutable evidence. Analysis scripts should operate on copies, indexed representations, or derived datasets rather than modifying original logs. This separation supports reproducibility and permits future reprocessing when algorithms, calibration parameters, or investigation questions change. Checksums, access controls, and controlled retention policies can further protect the integrity of important validation records.

The preprocessing stage converts heterogeneous logs into synchronized and interpretable data. Typical operations include message decoding, unit normalization, timestamp alignment, coordinate transformation, calibration application, event extraction, and sensor-quality checks. Preprocessing should be deterministic and version-controlled so the same raw dataset and pipeline version produce the same analysis-ready output whenever the evaluation is repeated.

Coordinate-frame consistency is critical when trajectories, maps, detections, and external references are combined. Transformations among sensor frames, robot base, odometry, local map, global map, GNSS coordinates, motion-capture coordinates, and external cameras should be validated before calculating spatial error. A transformation error can appear as poor localization or control performance even when the underlying robot behavior was correct.

Data-quality analysis should identify missing samples, irregular sampling, duplicate messages, timestamp discontinuities, sensor saturation, dropped video frames, corrupted files, invalid transforms, and periods of synchronization loss. These conditions should be explicitly marked rather than silently interpolated away. The analysis must distinguish robot failures from measurement failures because both can produce similar patterns in downstream KPI results.

Once preprocessing is complete, feature extraction converts low-level telemetry into quantities useful for validation. Trajectory error, stopping distance, minimum obstacle clearance, intervention duration, foot-slip events, actuator loading, task cycle time, energy consumption, communication outages, or recovery latency can be derived from synchronized signals. Derived quantities should retain references to the source intervals and processing algorithms that produced them.

KPI computation should use formally defined equations and event semantics shared across the campaign. Mission success, localization accuracy, path efficiency, fall rate, recovery success, task completion time, energy per mission, communication reliability, or safety-event frequency should be calculated consistently across trials. Changes to KPI definitions should be versioned because modifying a formula can alter apparent performance even when the underlying robot has not changed.

Automated analysis should be supplemented by targeted visualization and event replay. Time-series plots, trajectory overlays, synchronized sensor playback, video review, state-transition inspection, and three-dimensional reconstruction can reveal relationships that aggregate metrics cannot show. Visualization is particularly useful around anomalies, where a short sequence of perception, planning, control, and physical events may explain an otherwise unexplained KPI deviation.

Anomaly detection should identify trials or time intervals that differ significantly from expected operation. Threshold rules can detect excessive temperature, localization error, packet loss, vibration, control saturation, or latency, while statistical methods can identify unusual multivariate patterns. Automated anomaly detection should prioritize investigation rather than automatically assign root cause, because abnormal measurements can originate from the robot, environment, instrumentation, or data pipeline.

Failure analysis should reconstruct causal sequences from synchronized evidence. Investigators may trace an event from sensor degradation through incorrect perception, state-estimation uncertainty, planning behavior, control response, and eventual safety intervention or mission failure. Maintaining causal ordering is essential because the final visible failure may occur considerably later than the initiating condition and may involve several interacting subsystems.

Comparative analysis should support evaluation across software releases, hardware revisions, AI models, environments, and operating conditions. A common schema allows engineers to compare KPI distributions rather than isolated averages and determine whether a new configuration improves one capability while degrading another. Regression analysis should highlight statistically or operationally meaningful changes and link them back to representative field trials.

Large field campaigns require scalable indexing and retrieval. Engineers should be able to query trials by platform, scenario, date, configuration, environment, event type, failure category, or KPI range. Searchable metadata and standardized schemas reduce the time required to locate relevant evidence and enable rare failures to be studied across many hours of operation instead of remaining isolated incidents in individual log directories.

The analysis pipeline should generate traceable outputs suitable for engineering review. Reports should identify the source dataset, preprocessing version, KPI implementation, excluded intervals, anomaly classifications, and acceptance criteria associated with each conclusion. When a result supports release approval, safety assessment, or certification evidence, reviewers should be able to navigate from the reported metric back to the original trial and raw evidence.

Field data should also feed subsequent development activities. Difficult scenarios can become simulation cases, failed behaviors can become regression tests, unusual sensor conditions can become fault-injection experiments, and representative recordings can support perception or policy improvement. In this way, field testing becomes a feedback mechanism connecting real-world operation with software development, simulation, HIL testing, and future validation campaigns.

A mature logging and analysis pipeline therefore forms the evidence backbone of field testing. It preserves synchronized raw observations, experimental context, processing provenance, derived metrics, anomalies, and engineering conclusions in a reproducible chain. For AMRs, quadrupeds, humanoids, and UAVs alike, this pipeline converts complex real-world behavior into measurable evidence that can support debugging, benchmarking, safety evaluation, regression analysis, and deployment decisions.

현장 시험 데이터 로깅(Field-Test Data Logging)은 실제 로봇 운용을 완전하고 재현 가능한 디지털 기록(Digital Record)으로 변환해야 한다. 파이프라인은 단순히 임무의 성공 여부뿐만 아니라 그 결과를 만들어낸 인지, 추정, 계획, 제어, 안전, 통신 및 물리적 이벤트의 전체 순서를 기록해야 한다. 따라서 로깅은 현장 시험이 이미 시작된 이후 추가하는 기능이 아니라 검증 목표(Validation Objectives)와 핵심성과지표(KPI) 요구사항을 기반으로 사전에 설계해야 한다.

현장 데이터 파이프라인(Field-Data Pipeline)은 일반적으로 로봇과 시험 환경 전체에 분산된 이질적인 데이터 소스에서 시작한다. 여기에는 카메라, 라이다(LiDAR), 레이더, 관성측정장치(IMU), 위성항법시스템(GNSS), 관절 엔코더, 모터 제어기, 안전 장치, 네트워크 모니터, 환경 센서, 외부 정답 시스템(Ground-Truth System), 운영자 콘솔 및 동기화된 영상이 포함될 수 있다. 위치추정, 지도, 궤적, 객체 탐지, 정책 행동, 진단 및 임무 상태와 같은 소프트웨어 출력도 관련 원시 측정값과 함께 기록해야 한다.

로깅 아키텍처(Logging Architecture)는 고대역폭 센서 스트림과 상대적으로 낮은 전송률의 상태, 이벤트 및 진단 정보를 구분해야 한다. 원시 이미지와 포인트 클라우드(Point Cloud)는 전용 저장 경로가 필요할 수 있으며, 제어 명령, 자세, 안전 이벤트 및 시스템 상태 지표는 구조화된 메시지 로그를 사용할 수 있다. 엔지니어가 수동으로 정렬된 파일이나 불완전한 운영자 기록에 의존하지 않고 시스템 동작을 재구성할 수 있도록 이러한 데이터 소스 사이의 관계를 보존해야 한다.

시간 동기화(Time Synchronization)는 의미 있는 분석을 위한 기본 조건이다. 센서 획득, 인지 출력, 플래너(Planner) 결정, 제어기 명령, 액추에이터 응답, 안전 이벤트 및 외부 관측은 수 밀리초 이내에 연속적으로 발생할 수 있다. 따라서 필요한 경우 정밀 시간 프로토콜(PTP), 위성항법시스템 기반 시간, 하드웨어 트리거(Hardware Trigger) 또는 검증된 다른 동기화 메커니즘을 기반으로 공통 시계를 사용해야 하며, 예상되는 시간 정확도를 각 시험 구성과 함께 문서화해야 한다.

동일하게 보이는 타임스탬프도 데이터 경로의 서로 다른 단계를 나타낼 수 있으므로 타임스탬프 의미체계(Timestamp Semantics)를 보존해야 한다. 카메라 프레임에는 노출 시각, 드라이버 수신 시각, 미들웨어 발행 시각, 처리 시각 및 저장 시각이 각각 존재할 수 있다. 지연시간 분석에서는 실제 측정 대상 이벤트에 해당하는 타임스탬프를 사용해야 한다. 그렇지 않으면 버퍼링, 스케줄링 지터(Scheduling Jitter), 네트워크 지연 또는 처리 대기열로 인해 시스템 응답에 대한 잘못된 결론이 도출될 수 있다.

각 현장 시험을 시작하기 전에 로깅 시스템은 필수 채널이 활성화되어 있고 저장 자원이 충분한지를 검증해야 한다. 센서 스트림 가용성, 예상 메시지 전송률, 시계 동기화, 디스크 용량, 쓰기 처리량, 네트워크 연결, 메타데이터 완전성 및 외부 기록 장치 상태 등을 점검할 수 있다. 로봇 자체가 정상적으로 작동하는 것처럼 보이더라도 필수 증거를 신뢰성 있게 수집할 수 없다면 중요한 검증 시험을 시작해서는 안 된다.

데이터 전송률 계획(Data-Rate Planning)은 센서가 많은 로봇 시스템에서 특히 중요하다. 여러 대의 고해상도 카메라, 고밀도 라이다, 레이더, 오디오, 진단 추적 데이터 및 인공지능 출력은 저장장치나 네트워크의 처리 능력을 초과하는 지속적인 데이터 전송량을 발생시킬 수 있다. 엔지니어는 정상 및 최대 처리량을 추정하고 장시간 시험을 위한 여유 용량을 확보하며, 대표적인 부하 조건에서 기록 시스템을 시험하여 프레임 손실이나 프로세스 정체로 시험 캠페인이 무효화되지 않도록 해야 한다.

로깅은 측정 대상 시스템의 동작 자체를 크게 변화시키지 않도록 설계해야 한다. 압축, 직렬화(Serialization), 디스크 쓰기, 네트워크 전송 및 진단 추적은 연산 자원, 메모리, 대역폭 및 전력을 소비한다. 과도한 계측은 정상적인 배치 환경에서는 존재하지 않을 지연시간이나 열 부하를 발생시킬 수 있다. 따라서 로깅 오버헤드(Logging Overhead)를 측정하고 제한해야 하며 성능에 영향을 줄 가능성이 있다면 구성 기록에 포함해야 한다.

각 시험에는 원시 데이터를 해당 실험 맥락과 연결하는 고유 식별자(Unique Identifier)를 부여해야 한다. 메타데이터에는 시험 캠페인, 시나리오, 로봇 식별자, 하드웨어 구성, 소프트웨어 릴리스, 인공지능 모델 버전, 지도, 탑재물(Payload), 운영자, 환경 조건, 시작 및 종료 시각, 프로토콜 개정 버전 등을 포함해야 한다. 일관된 메타데이터는 데이터세트가 엔지니어링 의미를 재구성할 수 없는 익명의 파일 집합으로 변하는 것을 방지한다.

이벤트 로깅(Event Logging)은 연속적인 텔레메트리(Telemetry) 위에 간결한 의미 계층(Semantic Layer)을 제공한다. 임무 시작, 목표 도달, 위치추정 손실, 장애물 탐지, 재계획, 운영자 개입, 보호 정지(Protective Stop), 비상 정지(Emergency Stop), 복구, 작업 실패 및 임무 완료와 같은 이벤트는 표준화된 정의를 사용해야 한다. 이러한 이벤트 표시는 자동 분석 도구가 장시간 기록을 구간별로 분리하고 지속시간, 빈도, 상태 전이 및 결과 통계를 일관되게 계산할 수 있도록 한다.

운영자 관찰(Operator Observation)은 별도의 비공식 메모로만 관리하지 않고 데이터 파이프라인에 통합해야 한다. 시험 담당자는 휠 슬립(Wheel Slip), 비정상적인 진동, 예상하지 못한 사람의 행동, 환경 변화, 시야 가림, 비정상적인 소음 또는 물리적 접촉과 같이 온보드 진단 시스템이 식별하지 못하는 현상을 관찰할 수 있다. 타임스탬프가 포함된 주석을 사용하면 이러한 관찰 내용을 검색하고 분석 과정에서 로봇 텔레메트리 및 동기화된 영상과 연계할 수 있다.

시험 직후 수집 단계(Ingestion Stage)에서는 예상된 파일과 데이터 스트림이 성공적으로 기록되었는지를 검증해야 한다. 파일 무결성, 기록 시간, 메시지 개수, 타임스탬프, 메타데이터, 영상 파일의 정상 재생 여부 및 외부 기준 데이터를 자동으로 점검할 수 있다. 시험 구성이 그대로 유지되는 동안 누락된 증거를 발견하면 장비, 날씨, 지형 또는 소프트웨어 조건이 변경되기 전에 해당 시험을 다시 수행할 수 있다.

원시 데이터(Raw Data)는 일반적으로 변경할 수 없는 증거(Immutable Evidence)로 보존해야 한다. 분석 스크립트는 원본 로그를 수정하지 않고 복사본, 색인된 표현 또는 파생 데이터세트(Derived Dataset)를 대상으로 실행해야 한다. 이러한 분리는 재현성을 지원하며 알고리즘, 보정 매개변수 또는 조사 목적이 변경된 경우에도 향후 데이터를 다시 처리할 수 있게 한다. 체크섬(Checksum), 접근 제어 및 통제된 보존 정책을 사용하면 중요한 검증 기록의 무결성을 더욱 강화할 수 있다.

전처리 단계(Preprocessing Stage)는 이질적인 로그를 시간적으로 동기화되고 해석 가능한 데이터로 변환한다. 일반적인 처리에는 메시지 디코딩, 단위 정규화, 타임스탬프 정렬, 좌표 변환, 보정 적용, 이벤트 추출 및 센서 품질 검사가 포함된다. 전처리 과정은 결정론적(Deterministic)이고 버전 관리되어야 하며, 동일한 원시 데이터세트와 동일한 파이프라인 버전을 사용하면 평가를 반복할 때마다 동일한 분석 준비 결과가 생성되어야 한다.

궤적, 지도, 객체 탐지 결과 및 외부 기준 정보를 결합할 때 좌표 프레임 일관성(Coordinate-Frame Consistency)이 매우 중요하다. 센서 프레임, 로봇 베이스, 오도메트리(Odometry), 로컬 지도, 글로벌 지도, 위성항법 좌표, 모션 캡처(Motion Capture) 좌표 및 외부 카메라 사이의 변환 관계를 공간 오차 계산 전에 검증해야 한다. 좌표 변환 오류는 실제 로봇 동작이 정상적인 경우에도 위치추정이나 제어 성능이 저하된 것처럼 나타날 수 있다.

데이터 품질 분석(Data-Quality Analysis)은 누락된 샘플, 불규칙한 샘플링, 중복 메시지, 타임스탬프 불연속, 센서 포화, 영상 프레임 손실, 손상된 파일, 유효하지 않은 좌표 변환 및 동기화 손실 구간을 식별해야 한다. 이러한 조건을 임의로 보간하여 숨기지 않고 명시적으로 표시해야 한다. 로봇 장애와 측정 시스템 장애는 이후 핵심성과지표 결과에서 유사한 패턴을 만들 수 있으므로 분석 과정에서 두 가지를 명확히 구분해야 한다.

전처리가 완료되면 특징 추출(Feature Extraction)을 통해 저수준 텔레메트리를 검증에 유용한 물리량으로 변환한다. 궤적 오차, 정지 거리, 최소 장애물 이격 거리, 개입 지속시간, 발 미끄러짐 이벤트, 액추에이터 부하, 작업 주기 시간, 에너지 소비, 통신 중단 또는 복구 지연시간 등을 동기화된 신호로부터 도출할 수 있다. 파생된 물리량은 해당 값을 생성한 원본 데이터 구간과 처리 알고리즘에 대한 참조를 유지해야 한다.

핵심성과지표 계산(KPI Computation)은 시험 캠페인 전체에서 공유되는 공식적으로 정의된 계산식과 이벤트 의미체계를 사용해야 한다. 임무 성공률, 위치추정 정확도, 경로 효율성, 낙상률, 복구 성공률, 작업 완료 시간, 임무당 에너지, 통신 신뢰성 또는 안전 이벤트 빈도 등을 시험 간에 일관된 방식으로 계산해야 한다. 계산식 변경만으로 실제 로봇이 변하지 않았음에도 성능이 달라진 것처럼 나타날 수 있으므로 핵심성과지표 정의의 변경 사항도 버전 관리해야 한다.

자동화된 분석(Automated Analysis)은 목적에 맞는 시각화 및 이벤트 재생(Event Replay)과 함께 사용해야 한다. 시계열 그래프, 궤적 중첩, 동기화된 센서 재생, 영상 검토, 상태 전이 분석 및 3차원 재구성은 종합 지표만으로는 확인하기 어려운 관계를 보여줄 수 있다. 특히 이상 현상 주변에서는 인지, 계획, 제어 및 물리적 이벤트의 짧은 연속 과정이 설명하기 어려운 핵심성과지표 편차의 원인을 밝혀낼 수 있다.

이상 탐지(Anomaly Detection)는 예상되는 정상 운용과 상당히 다른 시험 또는 시간 구간을 식별해야 한다. 임계값 기반 규칙을 사용하여 과도한 온도, 위치추정 오차, 패킷 손실, 진동, 제어 포화 또는 지연시간을 탐지할 수 있으며, 통계적 방법을 이용하여 비정상적인 다변량 패턴을 식별할 수도 있다. 자동 이상 탐지는 근본 원인을 자동으로 단정하기보다 조사 우선순위를 결정하는 데 활용해야 한다. 비정상 측정값은 로봇, 환경, 계측 또는 데이터 파이프라인에서 발생할 수 있기 때문이다.

장애 분석(Failure Analysis)은 시간 동기화된 증거를 기반으로 인과관계의 연속 과정을 재구성해야 한다. 조사자는 센서 성능 저하에서 시작하여 잘못된 인지, 상태 추정 불확실성, 경로 계획 동작, 제어 응답, 최종적인 안전 개입 또는 임무 실패까지 이벤트를 추적할 수 있다. 최종적으로 관찰되는 장애는 최초 원인이 발생한 시점보다 상당히 늦게 나타날 수 있고 여러 하위 시스템의 상호작용을 포함할 수 있으므로 인과 순서(Causal Ordering)를 유지하는 것이 중요하다.

비교 분석(Comparative Analysis)은 소프트웨어 릴리스, 하드웨어 개정 버전, 인공지능 모델, 환경 및 운용 조건 간의 평가를 지원해야 한다. 공통 데이터 스키마(Common Schema)를 사용하면 개별 평균값이 아니라 핵심성과지표의 분포를 비교하고 새로운 구성이 한 기능을 개선하면서 다른 기능을 저하시키는지를 확인할 수 있다. 회귀 분석(Regression Analysis)은 통계적으로 또는 운용상 의미 있는 변화를 식별하고 이를 대표적인 현장 시험과 연결해야 한다.

대규모 현장 시험 캠페인에서는 확장 가능한 색인 및 검색(Scalable Indexing and Retrieval)이 필요하다. 엔지니어는 플랫폼, 시나리오, 날짜, 구성, 환경, 이벤트 유형, 장애 범주 또는 핵심성과지표 범위를 기준으로 시험 데이터를 검색할 수 있어야 한다. 검색 가능한 메타데이터와 표준화된 스키마를 사용하면 관련 증거를 찾는 시간을 줄이고 개별 로그 디렉터리의 고립된 사건으로 남을 수 있는 희귀 장애를 수많은 운용 시간에 걸쳐 분석할 수 있다.

분석 파이프라인(Analysis Pipeline)은 엔지니어링 검토에 사용할 수 있는 추적 가능한 결과를 생성해야 한다. 보고서에는 각 결론과 관련된 원본 데이터세트, 전처리 버전, 핵심성과지표 구현 버전, 제외된 데이터 구간, 이상 현상 분류 및 허용 기준을 명시해야 한다. 결과가 릴리스 승인, 안전성 평가 또는 인증 증거(Certification Evidence)에 사용되는 경우 검토자가 보고된 지표에서 최초 시험과 원시 증거까지 역으로 추적할 수 있어야 한다.

현장 데이터는 이후의 개발 활동에도 활용해야 한다. 어려운 시나리오는 시뮬레이션 사례로 전환할 수 있고, 실패한 동작은 회귀 시험(Regression Test)으로 만들 수 있으며, 비정상적인 센서 조건은 결함 주입 시험(Fault-Injection Experiment)에 활용할 수 있고, 대표적인 기록 데이터는 인지 또는 정책 개선에 사용할 수 있다. 이러한 방식으로 현장 시험은 실제 환경 운용을 소프트웨어 개발, 시뮬레이션, 하드웨어 인 더 루프 시험(HIL Testing) 및 향후 검증 캠페인과 연결하는 피드백 메커니즘(Feedback Mechanism)이 된다.

성숙한 로깅 및 분석 파이프라인(Logging and Analysis Pipeline)은 현장 시험의 증거 기반(Evidence Backbone)을 형성한다. 이 파이프라인은 시간 동기화된 원시 관측값, 실험 맥락, 처리 이력(Process Provenance), 파생 지표, 이상 현상 및 엔지니어링 결론을 재현 가능한 하나의 연속된 체계로 보존한다. 자율이동로봇(AMR), 사족보행 로봇(Quadruped), 휴머노이드(Humanoid), 무인항공기(UAV) 모두에서 이러한 파이프라인은 복잡한 실제 환경 동작을 디버깅, 벤치마킹, 안전성 평가, 회귀 분석 및 배치 의사결정을 지원할 수 있는 측정 가능한 증거로 변환한다.

##  

## 05.09. Field Test Incident Reporting and RCA

![](images/image9.png){width="7.268055555555556in" height="7.268055555555556in"}

Field-test incident reporting provides a disciplined mechanism for capturing abnormal events that occur during real-world robot validation. An incident may include collision, near miss, unexpected stop, loss of control, localization failure, fall, communication loss, safety-function activation, hardware damage, or human intervention. Reporting should preserve evidence and operational context rather than merely assign a short failure description.

The definition of an incident should be established before a test campaign begins. Teams should distinguish normal test failures, anomalies, safety-relevant events, near misses, equipment damage, and events requiring immediate escalation. A predefined classification scheme prevents serious observations from being dismissed as ordinary test noise and enables consistent comparison of incidents across AMR, quadruped, humanoid, UAV, and other robotic platforms.

Personnel should report incidents as soon as practical after the test environment has been made safe. Immediate priorities are protecting people, placing the robot in a safe state, preventing secondary damage, and preserving the scene when useful. Troubleshooting or restarting equipment should not destroy volatile evidence before essential logs, configuration states, photographs, video, operator observations, and physical conditions have been captured.

Each incident should receive a unique identifier linked to the associated campaign, test case, trial, robot, and configuration. The initial record should document time, location within the test environment, operating mode, mission state, software and hardware versions, environmental conditions, payload, personnel involved, observed behavior, safety responses, damage, and immediate actions. Facts should be separated from assumptions so early interpretations do not become accepted as evidence.

Incident severity should reflect actual and potential consequences rather than only visible damage. An event without injury or equipment damage may still be significant if a safety barrier failed or a hazardous condition was narrowly avoided. Severity assessment can consider personnel exposure, collision energy, loss of containment, safety-function performance, mission impact, hardware damage, recurrence potential, and the amount of intervention required to regain a safe condition.

Near misses should be recorded with the same discipline as visible failures because they provide evidence about weak safety margins before an accident occurs. Examples include unexpectedly small separation from a person, unstable recovery that narrowly prevents a fall, delayed emergency response, unintended UAV boundary approach, or AMR braking that stops just before contact. Repeated near misses can reveal systematic weaknesses that mission-success statistics conceal.

Evidence preservation should begin immediately after classification. Relevant artifacts may include raw sensor data, ROS 2 or middleware logs, controller traces, safety-controller events, network captures, synchronized video, external tracking, operator commands, diagnostic reports, battery data, environmental measurements, and physical inspection results. Copies used for investigation should be separated from protected original evidence so later processing does not alter the primary record.

Configuration evidence is essential because an incident can rarely be understood from telemetry alone. Investigators should preserve parameter files, maps, calibration data, AI model versions, container or package versions, firmware, safety settings, mission definitions, and recent configuration changes. The objective is to reconstruct the exact system that produced the event rather than analyze a nominal configuration that only appears similar.

A preliminary timeline should reconstruct the event from normal operation through the initiating condition, system response, incident, and recovery. Synchronized timestamps allow investigators to correlate perception outputs, state estimates, planner decisions, controller commands, actuator behavior, safety events, network conditions, and external observations. The timeline should begin sufficiently before the visible failure because the initiating condition may have occurred much earlier.

Root Cause Analysis should distinguish the initiating cause from contributing conditions and final consequences. A collision, fall, or mission abort is normally an outcome rather than a root cause. The investigation may reveal a chain involving degraded sensing, incorrect state estimation, an unsuitable planning decision, delayed control response, and inadequate recovery. Breaking this chain into causal stages prevents corrective action from targeting only the final symptom.

RCA should examine technical, environmental, procedural, and human factors without assuming in advance that one category contains the answer. Technical factors can include software defects, model limitations, hardware faults, timing errors, calibration problems, or interface failures. Environmental factors may include lighting, terrain, weather, interference, or unexpected obstacles, while procedural factors can involve incomplete checks, ambiguous protocols, or inadequate test boundaries.

Human actions should be analyzed as part of the system context rather than automatically labeled as operator error. An incorrect command may have resulted from confusing interface feedback, unclear authority, excessive workload, incomplete training, or an unexpected robot state. Effective RCA asks why the action was reasonable or possible under the circumstances and whether system design or procedures should have prevented a single human action from producing a hazardous outcome.

Causal analysis can use techniques such as Five Whys, fault trees, event trees, causal graphs, or failure-mode reasoning, depending on incident complexity. The selected method should help investigators move from observations toward evidence-supported causal relationships. Formal tools should not replace engineering judgment, and a root cause should not be accepted simply because a diagram terminates at that point; supporting evidence must remain available.

Software incidents often require replay of the recorded execution path. Engineers may reconstruct sensor inputs, localization states, perception outputs, planning decisions, and controller commands to determine where behavior diverged from expectation. Deterministic replay is ideal when available, but differences caused by asynchronous execution, nondeterministic AI inference, network timing, or hardware state should be documented when exact reproduction cannot be achieved.

AI-related incidents require particular attention to the distinction between model behavior and surrounding system behavior. A perception model may produce an incorrect detection, but RCA should also examine confidence handling, temporal filtering, redundancy, planner assumptions, safety supervision, and fallback behavior. A single model error should not automatically produce a hazardous system outcome when the architecture is designed with appropriate defensive layers.

Safety-function performance should be examined independently from the initiating operational failure. If normal navigation or manipulation fails, investigators should determine whether protective stopping, speed limitation, emergency stop, geofencing, fall mitigation, return-to-home, or another safety mechanism responded as designed. An incident in which the primary function fails but the safety layer operates correctly differs fundamentally from one involving failure of both layers.

Reproduction testing should be performed only after the event is sufficiently understood to define safe conditions. Investigators may reproduce the incident in simulation, software-in-the-loop, HIL, a controlled laboratory environment, or eventually the field. Lower-risk environments should be preferred when they can answer the causal question. Reproduction should vary suspected factors systematically rather than repeatedly recreate the original hazardous event without a clear hypothesis.

Corrective actions should address verified causes and contributing factors. Actions may include software fixes, controller changes, improved perception models, revised safety thresholds, hardware modifications, calibration procedures, additional diagnostics, test-protocol changes, operator-interface improvements, or new training requirements. Each action should have an owner, verification method, and closure criterion so the RCA produces measurable engineering change rather than only documentation.

Corrective and preventive action should extend beyond the single observed scenario when the underlying weakness can occur elsewhere. A timing defect discovered during AMR obstacle avoidance may affect docking, while a humanoid contact-detection weakness may influence several manipulation tasks. Engineers should therefore evaluate the scope of impact across related functions, platforms, configurations, and operating conditions before declaring an incident isolated.

Every significant incident should generate appropriate regression coverage. Recorded field data can become a replay dataset, simulation scenario, HIL case, unit or integration test, fault-injection condition, or controlled field test. The purpose is to ensure that the identified failure can be detected automatically if it reappears. Regression evidence also verifies that a corrective change resolves the problem without introducing unacceptable behavior elsewhere.

Incident closure should require more than implementation of a proposed fix. The team should verify the corrective action under representative conditions, confirm that associated regression tests pass, reassess relevant safety risks, and determine whether affected field trials must be repeated. Closure documentation should link the original event, causal evidence, corrective actions, verification results, residual risks, and approval decision in one traceable chain.

Incident trends should be analyzed across the entire test campaign rather than treating every report independently. Recurring localization losses, communication interruptions, falls, protective stops, interventions, or thermal faults may indicate a systemic problem even when individual events have low severity. Trend analysis can use frequency, operating hours, distance, mission count, terrain exposure, or task cycles to normalize occurrence rates.

Lessons learned should feed back into requirements, design, simulation, testing, operational procedures, and future campaign planning. Incidents reveal where assumptions made during development differ from physical reality and therefore provide unusually valuable validation evidence. A mature organization treats reporting as a learning mechanism that strengthens engineering controls rather than as a process intended primarily to attribute blame.

A complete incident-management process therefore connects immediate response, evidence preservation, event reconstruction, RCA, corrective action, regression testing, and verified closure. Maintaining this chain allows field failures and near misses to become reusable engineering knowledge. Within robotics field testing, disciplined incident reporting and RCA are essential for improving safety, reliability, autonomy, and confidence before deployment into broader operational environments.

현장 시험 사고 보고(Field-Test Incident Reporting)는 실제 환경에서 로봇을 검증하는 과정에서 발생하는 비정상적인 이벤트를 체계적으로 기록하기 위한 절차를 제공한다. 사고에는 충돌, 아차 사고(Near Miss), 예상하지 못한 정지, 제어 상실, 위치추정 실패, 낙상, 통신 손실, 안전 기능 작동, 하드웨어 손상 또는 사람의 개입 등이 포함될 수 있다. 사고 보고는 단순한 장애 설명에 그치지 않고 관련 증거와 운용 맥락을 보존해야 한다.

사고(Incident)의 정의는 시험 캠페인을 시작하기 전에 수립해야 한다. 시험팀은 일반적인 시험 실패, 이상 현상(Anomaly), 안전 관련 이벤트, 아차 사고, 장비 손상 및 즉각적인 상위 보고가 필요한 이벤트를 구분해야 한다. 사전에 정의된 분류 체계(Classification Scheme)는 심각한 관찰 결과가 일반적인 시험 잡음으로 간주되는 것을 방지하고 자율이동로봇(AMR), 사족보행 로봇(Quadruped), 휴머노이드(Humanoid), 무인항공기(UAV) 및 기타 로봇 플랫폼 간의 사고를 일관되게 비교할 수 있게 한다.

시험 환경을 안전한 상태로 만든 후 가능한 한 신속하게 사고를 보고해야 한다. 즉각적인 우선순위는 사람을 보호하고, 로봇을 안전 상태(Safe State)로 전환하고, 추가적인 손상을 방지하며, 필요한 경우 사고 현장을 보존하는 것이다. 필수 로그, 시스템 구성 상태, 사진, 영상, 운영자 관찰 및 물리적 조건을 확보하기 전에 문제 해결이나 장비 재시작을 수행하여 휘발성 증거(Volatile Evidence)가 손실되지 않도록 해야 한다.

각 사고에는 관련 시험 캠페인, 시험 사례, 시험 실행, 로봇 및 시스템 구성과 연결되는 고유 식별자(Unique Identifier)를 부여해야 한다. 초기 기록에는 발생 시각, 시험 환경 내 위치, 운용 모드, 임무 상태, 소프트웨어 및 하드웨어 버전, 환경 조건, 탑재물(Payload), 관련 인원, 관찰된 동작, 안전 대응, 손상 및 즉각적인 조치를 기록해야 한다. 초기 해석이 사실처럼 받아들여지는 것을 방지하기 위해 확인된 사실과 가정을 명확하게 구분해야 한다.

사고 심각도(Incident Severity)는 눈에 보이는 손상만이 아니라 실제 및 잠재적인 결과를 반영해야 한다. 부상이나 장비 손상이 발생하지 않았더라도 안전 장벽(Safety Barrier)이 실패했거나 위험한 상황을 간신히 피했다면 중요한 사고가 될 수 있다. 심각도 평가는 사람의 위험 노출, 충돌 에너지, 격리 상태 상실, 안전 기능의 성능, 임무 영향, 하드웨어 손상, 재발 가능성 및 안전 상태를 회복하는 데 필요한 개입 수준 등을 고려할 수 있다.

아차 사고(Near Miss)는 실제 사고가 발생하기 전에 취약한 안전 여유도(Safety Margin)를 보여주는 증거이므로 눈에 보이는 장애와 동일한 수준의 체계성을 가지고 기록해야 한다. 사람과 예상보다 지나치게 가까워진 상황, 낙상을 가까스로 방지한 불안정한 복구, 지연된 비상 대응, 무인항공기의 의도하지 않은 경계 접근 또는 접촉 직전에 정지한 자율이동로봇의 제동 등이 대표적인 사례이다. 반복적인 아차 사고는 임무 성공률 통계만으로는 드러나지 않는 체계적인 취약점을 나타낼 수 있다.

증거 보존(Evidence Preservation)은 사고 분류 직후 시작해야 한다. 관련 증거에는 원시 센서 데이터, ROS 2 또는 미들웨어 로그, 제어기 추적 데이터, 안전 제어기 이벤트, 네트워크 캡처, 동기화된 영상, 외부 추적 데이터, 운영자 명령, 진단 보고서, 배터리 데이터, 환경 측정값 및 물리적 점검 결과 등이 포함될 수 있다. 조사에 사용하는 복사본은 보호된 원본 증거와 분리하여 이후 처리 과정에서 최초 기록이 변경되지 않도록 해야 한다.

시스템 구성 증거(Configuration Evidence)는 텔레메트리만으로 사고를 완전히 이해하기 어려운 경우가 많으므로 필수적이다. 조사자는 매개변수 파일, 지도, 보정 데이터, 인공지능 모델(AI Model) 버전, 컨테이너 또는 패키지 버전, 펌웨어, 안전 설정, 임무 정의 및 최근의 구성 변경 사항을 보존해야 한다. 목적은 단순히 유사해 보이는 표준 구성을 분석하는 것이 아니라 실제 사고를 발생시킨 정확한 시스템 상태를 재구성하는 것이다.

예비 타임라인(Preliminary Timeline)은 정상 운용에서 시작하여 최초 유발 조건, 시스템 대응, 사고 발생 및 복구에 이르는 전체 이벤트 흐름을 재구성해야 한다. 시간 동기화된 타임스탬프를 사용하면 인지 출력, 상태 추정, 플래너(Planner) 결정, 제어기 명령, 액추에이터 동작, 안전 이벤트, 네트워크 상태 및 외부 관찰을 서로 연계할 수 있다. 사고의 최초 원인이 눈에 보이는 장애보다 훨씬 이전에 발생했을 수 있으므로 타임라인은 최종 장애 발생 시점보다 충분히 앞선 시점부터 분석해야 한다.

근본 원인 분석(Root Cause Analysis, RCA)은 최초 유발 원인(Initiating Cause), 기여 조건(Contributing Condition) 및 최종 결과를 구분해야 한다. 충돌, 낙상 또는 임무 중단은 일반적으로 근본 원인이 아니라 결과이다. 조사 과정에서는 센싱 성능 저하, 잘못된 상태 추정, 부적절한 경로 계획 결정, 지연된 제어 응답 및 불충분한 복구로 이어지는 연쇄 과정을 발견할 수 있다. 이러한 과정을 인과 단계(Causal Stage)로 분리하면 최종 증상만을 대상으로 수정 조치를 수행하는 문제를 방지할 수 있다.

근본 원인 분석은 기술적, 환경적, 절차적 및 인적 요인을 모두 검토해야 하며 어느 한 범주에 원인이 있다고 사전에 가정해서는 안 된다. 기술적 요인에는 소프트웨어 결함, 모델 한계, 하드웨어 장애, 타이밍 오류, 보정 문제 또는 인터페이스 장애가 포함될 수 있다. 환경 요인에는 조명, 지형, 날씨, 간섭 또는 예상하지 못한 장애물이 포함될 수 있으며, 절차적 요인에는 불완전한 점검, 모호한 프로토콜 또는 부적절한 시험 경계가 포함될 수 있다.

사람의 행동(Human Action)은 자동적으로 운영자 오류(Operator Error)로 분류하지 않고 전체 시스템 맥락의 일부로 분석해야 한다. 잘못된 명령은 혼란스러운 인터페이스 피드백, 불명확한 권한, 과도한 작업 부하, 불충분한 교육 또는 예상하지 못한 로봇 상태로 인해 발생했을 수 있다. 효과적인 근본 원인 분석은 당시 상황에서 해당 행동이 왜 합리적이었거나 가능했는지를 확인하고, 하나의 사람 행동이 위험한 결과를 발생시키지 않도록 시스템 설계나 절차가 이를 방지했어야 하는지를 검토한다.

인과관계 분석(Causal Analysis)에는 사고의 복잡도에 따라 다섯 번의 왜(Five Whys), 결함 트리(Fault Tree), 이벤트 트리(Event Tree), 인과 그래프(Causal Graph) 또는 고장 모드 추론(Failure-Mode Reasoning) 등의 기법을 사용할 수 있다. 선택한 방법은 조사자가 관찰 결과에서 증거에 기반한 인과관계로 이동할 수 있도록 지원해야 한다. 공식적인 분석 도구가 엔지니어링 판단을 대체해서는 안 되며, 단순히 분석 다이어그램의 끝에 위치한다는 이유만으로 특정 요소를 근본 원인으로 판단해서는 안 된다. 이를 뒷받침하는 증거가 반드시 존재해야 한다.

소프트웨어 관련 사고는 기록된 실행 경로(Execution Path)를 재생하여 분석해야 하는 경우가 많다. 엔지니어는 센서 입력, 위치추정 상태, 인지 출력, 계획 결정 및 제어기 명령을 재구성하여 시스템 동작이 어느 시점에서 예상된 동작과 달라졌는지를 확인할 수 있다. 가능한 경우 결정론적 재생(Deterministic Replay)이 이상적이지만 비동기 실행, 비결정론적 인공지능 추론, 네트워크 타이밍 또는 하드웨어 상태로 인해 정확한 재현이 불가능한 경우 그 차이를 문서화해야 한다.

인공지능 관련 사고(AI-Related Incident)는 모델 동작과 주변 시스템 동작을 구분하여 분석하는 것이 특히 중요하다. 인지 모델이 잘못된 탐지 결과를 생성했더라도 근본 원인 분석에서는 신뢰도 처리, 시간적 필터링(Temporal Filtering), 중복성(Redundancy), 플래너의 가정, 안전 감독 및 대체 동작(Fallback Behavior)도 함께 검토해야 한다. 적절한 방어 계층(Defensive Layer)을 갖춘 시스템이라면 단일 모델 오류가 곧바로 위험한 시스템 결과로 이어져서는 안 된다.

안전 기능 성능(Safety-Function Performance)은 최초의 운용 장애와 독립적으로 평가해야 한다. 정상적인 내비게이션이나 조작 기능이 실패한 경우에도 조사자는 보호 정지, 속도 제한, 비상 정지, 지오펜싱(Geofencing), 낙상 완화, 자동 복귀(Return-to-Home) 또는 기타 안전 메커니즘이 설계된 대로 동작했는지를 확인해야 한다. 주요 기능은 실패했지만 안전 계층이 올바르게 작동한 사고와 주요 기능 및 안전 계층이 모두 실패한 사고는 근본적으로 다른 위험 특성을 가진다.

재현 시험(Reproduction Testing)은 안전한 조건을 정의할 수 있을 만큼 사고가 충분히 이해된 이후에만 수행해야 한다. 조사자는 시뮬레이션, 소프트웨어 인 더 루프(Software-in-the-Loop), 하드웨어 인 더 루프(HIL), 통제된 실험실 환경 또는 최종적으로 현장에서 사고를 재현할 수 있다. 인과관계에 대한 질문에 답할 수 있다면 위험도가 낮은 환경을 우선 사용해야 한다. 명확한 가설 없이 원래의 위험한 사고를 반복하기보다 의심되는 요인을 체계적으로 변화시키면서 재현해야 한다.

시정 조치(Corrective Action)는 검증된 원인과 기여 요인을 대상으로 해야 한다. 조치에는 소프트웨어 수정, 제어기 변경, 인지 모델 개선, 안전 임계값 조정, 하드웨어 변경, 보정 절차 개선, 추가 진단 기능, 시험 프로토콜 변경, 운영자 인터페이스 개선 또는 새로운 교육 요구사항 등이 포함될 수 있다. 근본 원인 분석이 단순한 문서 작성으로 끝나지 않고 측정 가능한 엔지니어링 변경으로 이어지도록 각 조치에는 담당자, 검증 방법 및 완료 기준을 정의해야 한다.

시정 및 예방 조치(Corrective and Preventive Action)는 근본적인 취약점이 다른 영역에서도 발생할 수 있다면 단일 사고 시나리오를 넘어 확대 적용해야 한다. 자율이동로봇의 장애물 회피 과정에서 발견된 타이밍 결함이 도킹에도 영향을 줄 수 있으며, 휴머노이드의 접촉 감지 취약점이 여러 조작 작업에 영향을 줄 수 있다. 따라서 사고를 독립적인 단일 사례로 종결하기 전에 관련 기능, 플랫폼, 시스템 구성 및 운용 조건 전체에 대한 영향 범위(Scope of Impact)를 평가해야 한다.

중요한 사고는 적절한 회귀 시험 범위(Regression Coverage)를 생성해야 한다. 기록된 현장 데이터를 재생 데이터세트, 시뮬레이션 시나리오, 하드웨어 인 더 루프 시험 사례, 단위 또는 통합 시험, 결함 주입 조건 또는 통제된 현장 시험으로 변환할 수 있다. 목적은 확인된 장애가 다시 발생할 경우 이를 자동으로 탐지할 수 있도록 하는 것이다. 또한 회귀 시험 증거는 시정 변경이 문제를 해결하면서 다른 영역에 허용할 수 없는 동작을 새롭게 발생시키지 않았음을 검증한다.

사고 종결(Incident Closure)은 제안된 수정 사항을 구현했다는 사실만으로 완료되어서는 안 된다. 시험팀은 대표적인 조건에서 시정 조치를 검증하고, 관련 회귀 시험이 통과했는지 확인하고, 관련 안전 위험을 다시 평가하며, 영향을 받은 현장 시험을 다시 수행해야 하는지를 판단해야 한다. 종결 문서는 최초 사고, 인과관계 증거, 시정 조치, 검증 결과, 잔여 위험(Residual Risk) 및 승인 결정을 하나의 추적 가능한 연속 관계로 연결해야 한다.

사고 추세(Incident Trend)는 각각의 보고서를 독립적으로 처리하는 데 그치지 않고 전체 시험 캠페인에서 분석해야 한다. 반복적인 위치추정 손실, 통신 중단, 낙상, 보호 정지, 운영자 개입 또는 열 관련 장애는 개별 사건의 심각도가 낮더라도 체계적인 문제를 나타낼 수 있다. 추세 분석에서는 운용 시간, 이동 거리, 임무 횟수, 지형 노출량 또는 작업 주기 등을 기준으로 발생 빈도를 정규화하여 비교할 수 있다.

교훈(Lessons Learned)은 요구사항, 설계, 시뮬레이션, 시험, 운용 절차 및 향후 시험 캠페인 계획에 다시 반영해야 한다. 사고는 개발 과정에서 수립된 가정과 실제 물리적 환경 사이의 차이를 보여주므로 매우 가치 있는 검증 증거를 제공한다. 성숙한 조직은 사고 보고를 책임을 추궁하기 위한 절차가 아니라 엔지니어링 통제 체계를 강화하기 위한 학습 메커니즘(Learning Mechanism)으로 활용한다.

완전한 사고 관리 프로세스(Incident-Management Process)는 즉각적인 대응, 증거 보존, 이벤트 재구성, 근본 원인 분석, 시정 조치, 회귀 시험 및 검증된 종결을 하나의 연속된 체계로 연결한다. 이러한 연결 관계를 유지하면 현장 장애와 아차 사고를 재사용 가능한 엔지니어링 지식으로 전환할 수 있다. 로봇 현장 시험에서 체계적인 사고 보고와 근본 원인 분석은 보다 광범위한 운용 환경에 배치하기 전에 안전성, 신뢰성, 자율성 및 시스템에 대한 신뢰도를 향상시키는 핵심적인 검증 활동이다.

##  

## 05.10. Certification Field Test Evidence Collection

![](images/image10.png){width="7.268055555555556in" height="7.268055555555556in"}

Certification-oriented field testing must produce evidence that demonstrates not only that a robotic system performed successfully, but also that the result was obtained under defined, controlled, and traceable conditions. Evidence collection therefore connects field execution with requirements, safety arguments, verification records, and compliance activities. The objective is to create records that an independent reviewer can understand, reproduce, and evaluate.

Evidence planning should begin before the field campaign rather than after testing has been completed. Each applicable requirement should be mapped to one or more verification methods, test scenarios, measurements, acceptance criteria, and required artifacts. This traceability allows engineers to determine which requirements have sufficient evidence, which remain partially covered, and which require additional laboratory, simulation, HIL, or field validation.

The certification evidence plan should define the intended operational configuration and operating domain. Robot hardware, software, firmware, AI models, sensors, payloads, communication systems, safety functions, maps, infrastructure, and environmental assumptions should be identified. Evidence collected from a substantially different configuration may not support the intended certification claim unless equivalence or the impact of the differences can be justified.

Test procedures should be controlled documents with identifiable revisions and approval status. A procedure should define objectives, prerequisites, equipment, test environment, initial conditions, execution steps, required measurements, safety precautions, termination conditions, and acceptance criteria. Changes introduced during execution should be documented because an undocumented deviation can weaken the relationship between the approved procedure and the resulting evidence.

Field-test environments should be characterized sufficiently to demonstrate that they represent the conditions associated with the requirement being verified. Relevant properties may include terrain, slope, floor condition, lighting, weather, temperature, visibility, pedestrian density, obstacle geometry, communication coverage, GNSS quality, or airspace boundaries. Environmental measurements should accompany results whenever performance or safety depends materially on those conditions.

Instrumentation used to generate certification evidence should have known accuracy, range, resolution, sampling rate, synchronization quality, and calibration status. Measurement uncertainty should be considered when acceptance thresholds are close to observed values. External reference systems may be required for position, speed, stopping distance, force, trajectory, timing, or environmental measurements when onboard estimates cannot provide sufficiently independent evidence.

Time synchronization is particularly important when certification claims depend on event sequence or response time. Sensor detection, safety logic activation, control commands, actuator response, physical motion, and final stopping state may occur within short intervals. A documented timing architecture using validated clocks, PTP, GNSS timing, hardware triggers, or equivalent mechanisms enables reviewers to verify latency and response-time claims from synchronized records.

Before each test, configuration evidence should establish exactly what system is being evaluated. Records should identify serial numbers where relevant, hardware revisions, software commits or releases, parameter sets, firmware versions, AI model versions, calibration files, safety settings, payload condition, battery configuration, and mission definition. Automated configuration snapshots can reduce transcription errors and strengthen repeatability across multiple field trials.

Test readiness records should demonstrate that prerequisites were satisfied before execution. These records may include preflight or pre-operation inspections, calibration checks, communication checks, safety-function checks, battery status, sensor health, environmental limits, exclusion-zone confirmation, and personnel authorization. A successful test has limited certification value if there is no evidence that the required initial conditions were actually established.

During execution, raw measurements should be preserved together with higher-level events and observations. Sensor streams, state estimates, controller outputs, safety events, actuator telemetry, communication statistics, mission states, operator actions, external measurements, photographs, and synchronized video may all contribute to the evidence package. Raw data enables later verification of derived metrics and protects against dependence on a single interpretation of the trial.

Operator and witness records should identify who performed, supervised, and observed the test. Roles, qualifications where required, timestamps, deviations, interventions, and significant observations should be documented. For higher-assurance activities, independent witnessing or review may strengthen confidence that the procedure was followed correctly and that the reported outcome reflects what occurred during the test.

Acceptance criteria should be defined before the result is known. Criteria may address success rate, positioning accuracy, stopping distance, minimum separation, response latency, communication availability, task completion, endurance, stability, recovery, or safety-function behavior. Predefined criteria reduce the risk of selecting favorable interpretations after testing and allow pass, fail, conditional pass, or invalid outcomes to be assigned consistently.

A test result should include the calculated metric and sufficient information to reproduce that calculation. The source signals, time interval, filtering, coordinate frames, equations, software tool version, excluded samples, and uncertainty assumptions should be documented when relevant. Derived values without processing provenance provide weak evidence because reviewers cannot determine whether the reported KPI accurately represents the underlying physical event.

Evidence validity should be assessed independently from whether the robot appeared to perform successfully. Missing logs, synchronization loss, incorrect calibration, uncontrolled configuration changes, environmental excursions, instrumentation saturation, or procedural deviations may invalidate a trial. An invalid test should not be converted into a pass merely because the visible behavior appeared acceptable; it should be repeated or supported through an approved alternative method.

Failures and anomalies must remain part of the certification evidence record. Removing unsuccessful trials can create a misleading representation of reliability and operating limits. Each relevant anomaly should be linked to incident reporting, Root Cause Analysis, corrective action, and retest evidence where applicable. This creates a traceable history showing how identified weaknesses were understood and resolved before the final compliance claim.

Repeated trials should demonstrate that required performance is reproducible rather than the result of a favorable single run. The number of repetitions should reflect the requirement, variability, risk, and statistical confidence needed for the claim. Results should preserve distributions, worst cases, percentiles, and failure occurrences when these provide more meaningful evidence than averages alone, particularly for safety-related or autonomy-dependent behavior.

Boundary testing should provide evidence near the limits of the intended operating domain where appropriate and safe. Examples include maximum payload, representative speed limits, environmental extremes, difficult terrain, communication boundaries, low-energy conditions, or challenging human-interaction scenarios. The purpose is not to exceed approved safety constraints but to establish that the system remains compliant near declared operational boundaries.

Evidence from degraded and contingency conditions may be required in addition to nominal operation. Communication loss, sensor degradation, localization uncertainty, blocked routes, low battery, actuator faults, or unavailable task resources can trigger fallback behavior. Certification-oriented testing should demonstrate that these conditions are detected and that the robot transitions to a defined safe, degraded, recovery, or termination state consistent with its safety concept.

Safety-function evidence should remain distinguishable from normal functional-performance evidence. A navigation system may fail while an independent protective function correctly prevents collision. The evidence package should therefore demonstrate both the performance of the primary function and the effectiveness of relevant safety layers. Trigger conditions, response times, resulting states, reset requirements, and diagnostic events should be documented for safety-related functions.

Human intervention should be visible in certification records. Remote corrections, manual mode changes, physical assistance, emergency stops, object repositioning, or mission restarts can materially change the interpretation of a successful result. Evidence should distinguish autonomous completion from assisted completion and identify whether intervention was part of the approved procedure, an expected safety action, or an unplanned response to abnormal behavior.

Data integrity controls should protect certification evidence from accidental or unauthorized modification. Original logs can be retained as read-only records with checksums, controlled access, backup, and retention policies. Derived datasets and reports should reference their source records and processing versions. When evidence is transferred between systems or organizations, integrity verification should ensure that the reviewed material is identical to the approved source.

Evidence management should maintain bidirectional traceability between requirements and results. A reviewer should be able to start from a requirement and identify the procedure, configuration, trial, raw data, KPI calculation, anomaly status, and approval decision that support it. Conversely, every major field-test artifact should identify the requirement or verification objective it addresses so that large evidence repositories remain structured and auditable.

Changes after evidence collection require impact analysis. A software update, sensor replacement, mechanical modification, AI model retraining, parameter change, or safety-setting revision may invalidate some previously accepted results. Change-control processes should identify which requirements are affected and determine whether existing evidence remains applicable, requires analytical justification, or must be regenerated through regression or field testing.

Certification evidence should be assembled into reviewable packages rather than delivered as unstructured log archives. A package can contain the requirement reference, approved procedure, configuration record, environmental conditions, instrumentation information, execution record, raw-data references, analysis results, anomalies, corrective actions, and final disposition. Concise summaries should remain linked to detailed evidence so reviewers can inspect deeper levels when necessary.

Final evidence review should assess completeness, consistency, traceability, validity, and unresolved risk. Missing requirements, unexplained anomalies, inconsistent configurations, unsupported calculations, or open corrective actions should be identified before formal submission or approval. The objective is not merely to accumulate large quantities of data, but to establish a coherent argument supported by trustworthy and reproducible field observations.

A mature certification field-test process therefore creates an auditable chain from requirement to test method, system configuration, physical execution, raw measurement, analysis, acceptance decision, and retained evidence. For AMRs, quadrupeds, humanoids, and UAVs, this disciplined evidence collection transforms field testing from demonstration into objective verification and provides a defensible foundation for compliance assessment, safety assurance, certification, and deployment approval.

인증 중심 현장 시험(Certification-Oriented Field Testing)은 로봇 시스템이 성공적으로 동작했다는 사실뿐만 아니라 정의되고 통제되며 추적 가능한 조건에서 해당 결과가 획득되었음을 입증하는 증거를 생성해야 한다. 따라서 증거 수집(Evidence Collection)은 현장 시험 수행을 요구사항, 안전성 논증(Safety Argument), 검증 기록 및 규정 준수 활동과 연결한다. 목표는 독립적인 검토자가 이해하고 재현하며 평가할 수 있는 기록을 구축하는 것이다.

증거 계획(Evidence Planning)은 현장 시험이 완료된 이후가 아니라 시험 캠페인을 시작하기 전에 수립해야 한다. 적용 가능한 각 요구사항은 하나 이상의 검증 방법, 시험 시나리오, 측정 항목, 허용 기준 및 필수 산출물과 연결되어야 한다. 이러한 추적성(Traceability)을 통해 어떤 요구사항이 충분한 증거를 확보했는지, 어떤 요구사항이 부분적으로만 검증되었는지, 추가적인 실험실 시험, 시뮬레이션, 하드웨어 인 더 루프(HIL) 또는 현장 검증이 필요한지를 판단할 수 있다.

인증 증거 계획(Certification Evidence Plan)은 의도된 운용 구성과 운용 영역(Operating Domain)을 정의해야 한다. 로봇 하드웨어, 소프트웨어, 펌웨어, 인공지능 모델(AI Model), 센서, 탑재물(Payload), 통신 시스템, 안전 기능, 지도, 인프라 및 환경적 가정을 식별해야 한다. 상당히 다른 구성에서 수집된 증거는 구성 간 동등성 또는 차이가 미치는 영향을 정당화할 수 없는 경우 의도된 인증 주장(Certification Claim)을 뒷받침하지 못할 수 있다.

시험 절차(Test Procedure)는 식별 가능한 개정 버전과 승인 상태를 갖는 통제 문서(Controlled Document)로 관리해야 한다. 절차에는 시험 목표, 사전 조건, 장비, 시험 환경, 초기 조건, 실행 단계, 필수 측정값, 안전 예방조치, 종료 조건 및 허용 기준이 정의되어야 한다. 시험 수행 중 변경 사항이 발생한 경우 이를 문서화해야 하며, 기록되지 않은 절차 이탈(Deviation)은 승인된 절차와 최종 시험 증거 사이의 연관성을 약화시킬 수 있다.

현장 시험 환경(Field-Test Environment)은 검증 대상 요구사항과 관련된 조건을 대표한다는 사실을 입증할 수 있을 정도로 충분히 특성화해야 한다. 관련 특성에는 지형, 경사도, 바닥 상태, 조명, 날씨, 온도, 가시성, 보행자 밀도, 장애물 형상, 통신 커버리지, 위성항법시스템(GNSS) 품질 또는 공역 경계 등이 포함될 수 있다. 성능이나 안전성이 이러한 조건에 실질적으로 의존하는 경우 환경 측정값을 시험 결과와 함께 보존해야 한다.

인증 증거를 생성하는 데 사용되는 계측 장비(Instrumentation)는 알려진 정확도, 측정 범위, 분해능, 샘플링 속도, 동기화 품질 및 보정 상태를 가져야 한다. 측정된 값이 허용 임계값에 근접하는 경우 측정 불확도(Measurement Uncertainty)를 고려해야 한다. 온보드 추정값만으로 충분히 독립적인 증거를 제공할 수 없다면 위치, 속도, 정지 거리, 힘, 궤적, 시간 또는 환경 조건을 측정하기 위한 외부 기준 시스템(External Reference System)이 필요할 수 있다.

인증 주장이 이벤트 순서 또는 응답시간에 의존하는 경우 시간 동기화(Time Synchronization)는 특히 중요하다. 센서 탐지, 안전 로직 활성화, 제어 명령, 액추에이터 응답, 실제 물리적 움직임 및 최종 정지 상태는 매우 짧은 시간 간격으로 발생할 수 있다. 검증된 시계, 정밀 시간 프로토콜(PTP), 위성항법시스템 시간, 하드웨어 트리거(Hardware Trigger) 또는 이에 상응하는 메커니즘을 사용하는 문서화된 시간 체계는 검토자가 동기화된 기록을 통해 지연시간 및 응답시간에 대한 주장을 검증할 수 있게 한다.

각 시험을 수행하기 전에 구성 증거(Configuration Evidence)를 통해 정확히 어떤 시스템이 평가되는지를 확립해야 한다. 필요한 경우 일련번호, 하드웨어 개정 버전, 소프트웨어 커밋 또는 릴리스, 매개변수 세트, 펌웨어 버전, 인공지능 모델 버전, 보정 파일, 안전 설정, 탑재물 상태, 배터리 구성 및 임무 정의를 기록해야 한다. 자동화된 구성 스냅샷(Configuration Snapshot)을 사용하면 수동 기록 과정에서 발생하는 오류를 줄이고 여러 현장 시험 사이의 반복성을 강화할 수 있다.

시험 준비 기록(Test Readiness Record)은 시험 수행 전에 필요한 사전 조건이 충족되었음을 입증해야 한다. 이러한 기록에는 비행 전 또는 운용 전 점검, 보정 확인, 통신 점검, 안전 기능 확인, 배터리 상태, 센서 건전성, 환경 한계, 출입 제한 구역 확인 및 시험 인력의 권한 확인 등이 포함될 수 있다. 필요한 초기 조건이 실제로 확립되었다는 증거가 없다면 성공적으로 수행된 시험이라도 인증 관점에서 제한적인 가치만 가질 수 있다.

시험 수행 중에는 상위 수준의 이벤트 및 관찰 결과와 함께 원시 측정값(Raw Measurement)을 보존해야 한다. 센서 스트림, 상태 추정값, 제어기 출력, 안전 이벤트, 액추에이터 텔레메트리(Telemetry), 통신 통계, 임무 상태, 운영자 행동, 외부 측정값, 사진 및 동기화된 영상 등이 모두 증거 패키지(Evidence Package)에 포함될 수 있다. 원시 데이터는 이후 파생 지표를 다시 검증할 수 있게 하며 시험 결과가 하나의 해석에만 의존하는 것을 방지한다.

운영자 및 입회자 기록(Operator and Witness Record)은 시험을 수행하고 감독하며 관찰한 사람을 식별해야 한다. 필요한 경우 역할, 자격, 타임스탬프, 절차 이탈, 개입 및 중요한 관찰 사항을 기록해야 한다. 높은 수준의 보증(Assurance)이 요구되는 활동에서는 독립적인 입회 또는 검토를 통해 시험 절차가 올바르게 수행되었으며 보고된 결과가 실제 시험 중 발생한 상황을 정확하게 반영한다는 신뢰도를 높일 수 있다.

허용 기준(Acceptance Criteria)은 시험 결과가 확인되기 전에 정의해야 한다. 기준에는 성공률, 위치 정확도, 정지 거리, 최소 이격 거리, 응답 지연시간, 통신 가용성, 작업 완료 여부, 내구성, 안정성, 복구 능력 또는 안전 기능 동작 등이 포함될 수 있다. 사전에 정의된 기준은 시험 이후 유리한 해석을 선택할 가능성을 줄이고 합격(Pass), 불합격(Fail), 조건부 합격(Conditional Pass) 또는 무효(Invalid) 결과를 일관된 방식으로 판정할 수 있게 한다.

시험 결과에는 계산된 지표와 함께 해당 계산을 재현할 수 있는 충분한 정보를 포함해야 한다. 관련되는 경우 원본 신호, 분석 시간 구간, 필터링 방법, 좌표 프레임, 계산식, 소프트웨어 도구 버전, 제외된 샘플 및 불확도 가정을 문서화해야 한다. 처리 이력(Processing Provenance)이 없는 파생값은 검토자가 보고된 핵심성과지표(KPI)가 실제 물리적 이벤트를 정확하게 나타내는지 판단할 수 없으므로 증거로서의 신뢰도가 낮다.

증거 유효성(Evidence Validity)은 로봇이 외관상 성공적으로 동작했는지 여부와 독립적으로 평가해야 한다. 로그 누락, 시간 동기화 손실, 잘못된 보정, 통제되지 않은 구성 변경, 환경 조건의 허용 범위 이탈, 계측 장비 포화 또는 절차 이탈은 시험을 무효화할 수 있다. 눈으로 관찰한 동작이 허용 가능해 보인다는 이유만으로 무효 시험을 합격으로 처리해서는 안 되며, 시험을 다시 수행하거나 승인된 대체 방법으로 증거를 보완해야 한다.

실패 및 이상 현상(Failure and Anomaly)도 인증 증거 기록에 포함되어야 한다. 실패한 시험을 제거하면 시스템의 신뢰성과 운용 한계를 왜곡하여 보여줄 수 있다. 관련된 각 이상 현상은 필요한 경우 사고 보고(Incident Reporting), 근본 원인 분석(Root Cause Analysis), 시정 조치(Corrective Action) 및 재시험 증거와 연결해야 한다. 이를 통해 최종 규정 준수 주장 전에 발견된 취약점이 어떻게 분석되고 해결되었는지를 보여주는 추적 가능한 이력을 구축할 수 있다.

반복 시험(Repeated Trial)은 요구 성능이 우연히 유리한 한 번의 시험 결과가 아니라 재현 가능한 성능임을 입증해야 한다. 반복 횟수는 요구사항, 변동성, 위험도 및 해당 주장에 필요한 통계적 신뢰 수준을 반영해야 한다. 특히 안전 관련 또는 자율성 의존 동작에서는 평균값만 사용하는 것보다 결과 분포, 최악 조건, 백분위수(Percentile) 및 실패 발생 횟수를 보존하는 것이 더욱 의미 있는 증거를 제공할 수 있다.

경계 조건 시험(Boundary Testing)은 적절하고 안전한 경우 의도된 운용 영역의 한계에 가까운 조건에서 증거를 제공해야 한다. 최대 탑재물, 대표적인 속도 한계, 환경 극한 조건, 어려운 지형, 통신 경계, 낮은 에너지 상태 또는 까다로운 인간 상호작용 시나리오 등이 이에 포함될 수 있다. 목적은 승인된 안전 제약조건을 초과하는 것이 아니라 선언된 운용 경계 근처에서도 시스템이 규정 준수 상태를 유지하는지를 확인하는 것이다.

정상 운용(Nominal Operation)뿐만 아니라 성능 저하 및 비상 조건(Degraded and Contingency Conditions)에 대한 증거도 필요할 수 있다. 통신 손실, 센서 성능 저하, 위치추정 불확실성, 차단된 경로, 배터리 부족, 액추에이터 장애 또는 사용할 수 없는 작업 자원은 대체 동작(Fallback Behavior)을 유발할 수 있다. 인증 중심 시험은 이러한 상태가 올바르게 감지되고 로봇이 안전 개념(Safety Concept)에 부합하는 정의된 안전 상태, 성능 저하 상태, 복구 상태 또는 종료 상태로 전환되는지를 입증해야 한다.

안전 기능 증거(Safety-Function Evidence)는 정상 기능 성능에 대한 증거와 구분할 수 있어야 한다. 예를 들어 내비게이션 시스템이 실패하더라도 독립적인 보호 기능이 충돌을 올바르게 방지할 수 있다. 따라서 증거 패키지는 주요 기능의 성능과 관련 안전 계층의 유효성을 모두 입증해야 한다. 안전 관련 기능에 대해서는 작동 조건, 응답시간, 최종 상태, 재설정 요구사항 및 진단 이벤트를 문서화해야 한다.

사람의 개입(Human Intervention)은 인증 기록에서 명확하게 확인할 수 있어야 한다. 원격 수정, 수동 모드 변경, 물리적 지원, 비상 정지, 물체 재배치 또는 임무 재시작은 성공적인 시험 결과의 해석을 크게 변화시킬 수 있다. 증거에서는 완전 자율 완료(Autonomous Completion)와 지원을 통한 완료(Assisted Completion)를 구분하고, 해당 개입이 승인된 절차의 일부였는지, 예상된 안전 조치였는지 또는 비정상 동작에 대한 계획되지 않은 대응이었는지를 식별해야 한다.

데이터 무결성 통제(Data Integrity Control)는 인증 증거가 우발적이거나 승인되지 않은 방식으로 변경되는 것을 방지해야 한다. 원본 로그는 체크섬(Checksum), 접근 제어, 백업 및 보존 정책과 함께 읽기 전용 기록으로 유지할 수 있다. 파생 데이터세트와 보고서는 원본 기록과 처리 버전을 참조해야 한다. 조직이나 시스템 사이에서 증거를 전송하는 경우 무결성 검증을 통해 검토 대상 자료가 승인된 원본과 동일한지를 확인해야 한다.

증거 관리(Evidence Management)는 요구사항과 시험 결과 사이의 양방향 추적성(Bidirectional Traceability)을 유지해야 한다. 검토자는 특정 요구사항에서 시작하여 이를 지원하는 시험 절차, 시스템 구성, 시험 실행, 원시 데이터, 핵심성과지표 계산, 이상 현상 상태 및 승인 결정을 확인할 수 있어야 한다. 반대로 주요 현장 시험 산출물도 자신이 어떤 요구사항 또는 검증 목표를 지원하는지를 식별하여 대규모 증거 저장소가 구조적이고 감사 가능한 상태를 유지하도록 해야 한다.

증거 수집 이후 시스템이 변경되면 영향 분석(Impact Analysis)을 수행해야 한다. 소프트웨어 업데이트, 센서 교체, 기계적 변경, 인공지능 모델 재학습, 매개변수 변경 또는 안전 설정 수정으로 인해 이전에 승인된 일부 시험 결과가 더 이상 유효하지 않을 수 있다. 변경 관리(Change Control) 과정에서는 영향을 받는 요구사항을 식별하고 기존 증거를 계속 적용할 수 있는지, 분석적 정당화가 필요한지 또는 회귀 시험이나 현장 시험을 통해 증거를 다시 생성해야 하는지를 판단해야 한다.

인증 증거는 구조화되지 않은 대규모 로그 아카이브 형태가 아니라 검토 가능한 증거 패키지(Reviewable Evidence Package)로 구성해야 한다. 패키지에는 요구사항 참조, 승인된 시험 절차, 구성 기록, 환경 조건, 계측 정보, 시험 수행 기록, 원시 데이터 참조, 분석 결과, 이상 현상, 시정 조치 및 최종 판정이 포함될 수 있다. 간결한 요약 정보는 상세 증거와 연결되어 검토자가 필요한 경우 더 깊은 수준의 자료까지 확인할 수 있어야 한다.

최종 증거 검토(Final Evidence Review)는 완전성, 일관성, 추적성, 유효성 및 해결되지 않은 위험을 평가해야 한다. 누락된 요구사항, 설명되지 않은 이상 현상, 일관되지 않은 시스템 구성, 근거가 부족한 계산 또는 완료되지 않은 시정 조치는 공식적인 제출이나 승인 전에 식별해야 한다. 목적은 단순히 많은 양의 데이터를 축적하는 것이 아니라 신뢰할 수 있고 재현 가능한 현장 관측을 기반으로 일관된 인증 논증(Certification Argument)을 구축하는 것이다.

성숙한 인증 현장 시험 프로세스(Certification Field-Test Process)는 요구사항에서 시험 방법, 시스템 구성, 실제 시험 수행, 원시 측정값, 분석, 허용 여부 결정 및 보존된 증거로 이어지는 감사 가능한 연속 체계(Auditable Chain)를 구축한다. 자율이동로봇(AMR), 사족보행 로봇(Quadruped), 휴머노이드(Humanoid) 및 무인항공기(UAV)에서 이러한 체계적인 증거 수집은 현장 시험을 단순한 시연에서 객관적인 검증(Objective Verification)으로 전환하며, 규정 준수 평가, 안전성 보증(Safety Assurance), 인증 및 실제 배치 승인을 위한 방어 가능하고 신뢰성 있는 기반을 제공한다.
