**Volume 25. Testing Validation and Benchmarking**

# Chapter 01. Testing Fundamentals

## 01.01. Testing Pyramid Unit Integration System Field

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

테스트 피라미드(Testing Pyramid)는 작고 결정론적인 구성요소부터 실제 환경에서 작동하는 완전한 로봇에 이르기까지 로봇 소프트웨어(Robot Software)를 단계적으로 검증하기 위한 계층형 전략이다. 핵심 원칙은 빠르고 비용이 낮으며 고도로 격리된 테스트를 피라미드 하단에 많이 배치하고, 실행 시간이 길고 비용이 높으며 하드웨어(Hardware)와 환경 조건에 대한 의존성이 커질수록 테스트 수를 점진적으로 줄이는 것이다.

단위 테스트(Unit Testing)는 테스트 피라미드의 기반을 형성한다. 단위 테스트는 수학 함수, 상태 전이(State Transition), 제어기 계산, 좌표 변환(Coordinate Transformation), 메시지 파서(Message Parser), 궤적 제약조건(Trajectory Constraint), 안전 조건(Safety Condition)처럼 범위가 명확하게 정의된 소프트웨어 요소를 검증한다. 일반적으로 의존성은 모의 객체(Mock), 스텁(Stub), 픽스처(Fixture), 시뮬레이션 인터페이스(Simulated Interface)를 통해 격리하여 장애 원인을 해당 구성요소에 직접 귀속시킬 수 있도록 한다.

로보틱스(Robotics)에서 단위 테스트는 시뮬레이터(Simulator)를 실행하거나 실제 하드웨어를 연결하지 않고도 많은 알고리즘을 검증할 수 있기 때문에 특히 중요하다. 운동학(Kinematics) 계산, PID 제어기(PID Controller) 방정식, 필터링 함수, 충돌 판정 조건, 명령 제한기(Command Limiter), 센서 변환, 인지 전처리(Perception Preprocessing) 단계 등을 결정론적 입력과 예상 출력으로 검사할 수 있다. 빠른 실행 속도를 활용하면 소프트웨어가 변경될 때마다 수천 개의 검사를 수행할 수 있다.

통합 테스트(Integration Testing)는 개별 구성요소를 넘어 여러 모듈(Module) 사이의 상호작용을 검증하는 단계로 이동한다. 목표는 각각의 함수가 독립적으로 올바르게 동작하는지만 확인하는 것이 아니라, 구성요소가 함께 작동할 때 인터페이스(Interface), 타이밍 가정(Timing Assumption), 데이터 표현(Data Representation), 통신 프로토콜(Communication Protocol), 수명주기 동작(Lifecycle Behavior)이 올바르게 유지되는지를 확인하는 것이다. 독립적으로 정상인 모듈도 연결된 상태에서는 실패할 수 있는 분산 로봇 아키텍처(Distributed Robot Architecture)에서 특히 중요한 계층이다.

ROS 2 로봇은 이러한 차이를 명확하게 보여준다. 위치추정(Localization), 인지(Perception), 계획(Planning), 제어(Control) 노드(Node)가 각각 단위 테스트를 통과하더라도 호환되지 않는 서비스 품질(QoS), 잘못된 좌표 프레임(Coordinate Frame), 오래된 타임스탬프(Timestamp), 메시지 전송률 불일치, 네임스페이스(Namespace) 오류 또는 수명주기 순서 문제로 통합 시스템이 실패할 수 있다. 따라서 통합 테스트는 노드 그래프(Node Graph), 토픽(Topic), 서비스(Service), 액션(Action), 미들웨어(Middleware), API, 데이터베이스(Database) 및 기타 하위 시스템 경계를 검사한다.

시스템 테스트(System Testing)는 완전한 운용 시스템으로 구성된 로봇 소프트웨어를 시스템 수준 요구사항(System-Level Requirement)에 대해 평가한다. 대부분의 의존성을 테스트 대역(Test Double)으로 대체하는 대신 실제에 가까운 소프트웨어 구성과 가능한 경우 대표적인 하드웨어 또는 고충실도 시뮬레이션(High-Fidelity Simulation)을 결합한다. 테스트에서는 시스템 시작, 위치추정, 내비게이션(Navigation), 장애물 회피, 조작(Manipulation), 도킹(Docking), 장애 복구(Fault Recovery), 종료 또는 임무 완료와 같은 전체 작업 흐름을 실행할 수 있다.

시스템 수준 검증(System-Level Verification)은 구현 세부사항보다 외부에서 관찰할 수 있는 동작과 요구사항 충족 여부를 중점적으로 평가해야 한다. 예를 들어 자율이동로봇(Autonomous Mobile Robot)은 목표 지점 도달, 금지 영역 회피, 안전거리 유지, 위치추정 교란으로부터의 복구, 안전 조건 발생 시 정확한 정지 능력 등을 평가할 수 있다. 이 단계에서는 내부 알고리즘 자체보다 통합된 로봇이 정의된 운용 계약(Operational Contract)을 만족하는지가 더욱 중요하다.

시뮬레이션(Simulation)은 소프트웨어 통합과 물리적 시스템 테스트 사이를 연결하는 중요한 역할을 한다. 소프트웨어 인 더 루프(Software-in-the-Loop, SiL)와 모델 인 더 루프(Model-in-the-Loop, MiL) 환경에서는 물리적 테스트보다 훨씬 큰 규모로 반복 가능한 시나리오(Scenario)를 실행할 수 있으며, 고충실도 시뮬레이터는 내비게이션, 조작, 보행(Locomotion), 비행 소프트웨어를 다양한 환경 변화와 엣지 케이스(Edge Case)에 노출할 수 있다. 이러한 테스트 구조는 시나리오 기반 검증(Scenario-Based Validation)과 통계적 검증(Statistical Validation)으로 확장될 수 있다.

하드웨어 인 더 루프 테스트(Hardware-in-the-Loop Testing, HIL)는 실제 제어기(Controller), 인터페이스, 네트워크(Network) 또는 전자 구성요소를 시뮬레이션된 플랜트(Simulated Plant)와 센서 자극(Sensor Stimulus)에 연결함으로써 검증을 실제 물리적 시스템에 더욱 가깝게 이동시킨다. 완전한 로봇을 잠재적으로 위험한 조건에 노출하기 전에 타이밍 민감 동작, 모터 인터페이스, 센서 경로, 통신 버스(Communication Bus), 안전 기능 및 장애 대응을 검증하는 데 특히 유용하다. 이 계층은 시스템 테스트를 대체하는 것이 아니라 보완한다.

현장 테스트(Field Testing)는 로보틱스 테스트 피라미드에서 가장 높은 단계이며 일반적으로 가장 많은 비용이 요구된다. 로봇은 실험실 환경에서 완벽하게 재현하기 어려운 조명, 지형, 사람, 통신 품질, 온도, 진동, 객체 변화, 교통, 날씨 및 예기치 않은 상호작용이 존재하는 대표 환경 또는 실제 환경에서 작동한다. 따라서 현장 테스트는 소프트웨어, 하드웨어, 환경 및 인간 활동 사이의 복잡한 결합으로 발생하는 장애를 발견하는 역할을 한다.

체계적인 현장 테스트 캠페인(Field Test Campaign)은 비공식적인 시연이 아니라 명확한 범위, 프로토콜(Protocol), 계측(Instrumentation), 안전 통제(Safety Control), 측정 가능한 핵심성과지표(Key Performance Indicator, KPI), 데이터 수집 절차에서 시작해야 한다. 기록된 텔레메트리(Telemetry)를 통해 관찰된 동작을 소프트웨어 버전, 구성 매개변수(Configuration Parameter), 하드웨어 상태, 환경 조건 및 테스트 시나리오까지 추적할 수 있어야 한다. 이후 사고 보고(Incident Reporting)와 근본 원인 분석(Root Cause Analysis, RCA)을 통해 현장에서 발견된 장애를 재현 가능한 엔지니어링 증거와 회귀 테스트(Regression Test)로 전환한다.

피라미드의 형태는 기술적 원칙뿐만 아니라 경제적 원칙도 나타낸다. 단위 테스트는 지속적으로 실행할 수 있을 정도로 비용이 낮은 반면, 통합 테스트에는 더 많은 인프라(Infrastructure)가 필요하다. 시스템 테스트는 상당한 컴퓨팅 또는 실험실 자원을 소비하며, 현장 테스트는 실제 장비, 운영자, 안전 준비 및 시간을 요구한다. 따라서 동일한 결함이라도 피라미드 하단에서 발견하는 것이 현장 배포(Field Deployment) 단계에서 발견하는 것보다 일반적으로 진단 속도가 빠르고 수정 비용도 낮다.

각 테스트 계층을 서로 분리된 게이트(Gate)로 해석해서는 안 된다. 성숙한 로봇 개발 프로세스는 계층 전체에 걸쳐 추적성(Traceability)을 구축한다. 하나의 요구사항은 중요한 계산을 위한 단위 수준 검사, 인터페이스를 위한 통합 테스트, 전체 동작을 위한 시스템 시나리오, 운용 증거를 확보하기 위한 현장 절차로 이어질 수 있다. 상위 계층에서 결함이 발견되면 향후 회귀 문제를 더 빠르고 경제적으로 발견할 수 있도록 가능한 가장 낮은 계층에서 해당 결함을 재현하는 것이 바람직하다.

테스트의 분포는 로봇 플랫폼(Robot Platform)과 위험 프로파일(Risk Profile)에 따라서도 달라진다. 자율이동로봇(AMR)은 내비게이션, 위치추정, 장애물 상호작용 및 내구성(Endurance)을 강조할 수 있고, 다족보행로봇(Legged Robot)은 균형과 지형에 대한 광범위한 테스트가 필요하다. 휴머노이드(Humanoid)는 조작과 인간-로봇 상호작용(Human-Robot Interaction, HRI)이 추가되며, 무인항공기(Unmanned Aerial Vehicle, UAV)는 비행 제어, 항법, 이중화(Redundancy) 및 운용 안전 검증이 중요하다. 따라서 공통 테스트 기반은 궁극적으로 플랫폼별 테스트 전략으로 확장된다.

인공지능 기반 로봇(AI-Enabled Robot)은 학습된 구성요소가 확률적(Probabilistic)이며 데이터 분포(Data Distribution)에 민감하기 때문에 전통적인 테스트 피라미드를 더욱 복잡하게 만든다. 인지 또는 정책 모델(Policy Model)이 결정론적인 소프트웨어 인터페이스 테스트를 통과하더라도 익숙하지 않은 객체, 조명 조건, 장면 또는 물리적 상호작용에서는 실패할 수 있다. 따라서 기존의 단위 및 통합 테스트에 데이터셋 평가(Dataset Evaluation), 시나리오 커버리지(Scenario Coverage), 강건성 테스트(Robustness Testing), 시뮬레이션 캠페인 및 실제 환경 성능 측정을 추가해야 한다.

따라서 테스트 피라미드는 경직된 계층 구조가 아니라 지속적인 증거 아키텍처(Continuous Evidence Architecture)로 이해해야 한다. 단위 테스트, 통합 테스트, 시스템 테스트, 시뮬레이션, 하드웨어 인 더 루프 테스트 및 현장 테스트는 로봇을 점진적으로 더 높은 상호작용 복잡성과 물리적 현실성(Physical Realism)에 노출한다. 이러한 계층을 함께 적용함으로써 소프트웨어 구성요소의 정확성, 하위 시스템 간 협력, 전체 시스템의 요구사항 충족, 실제 운용 조건에서 배포된 로봇의 신뢰성을 종합적으로 입증할 수 있다.

## 01.02. V Model for Robot SW Development and Testing

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

V-모델(V-Model)은 로봇 소프트웨어(Robot Software) 개발 활동과 이에 대응하는 검증 및 유효성 확인(Verification and Validation) 활동을 연결하기 위한 체계적인 프레임워크(Framework)를 제공한다. 왼쪽은 운용 요구사항(Operational Needs)에서 세부 구현(Implementation)으로 점진적으로 분해되는 과정을 나타내며, 오른쪽은 점진적인 통합(Integration)과 테스트(Test)를 나타낸다. 따라서 각 개발 산출물은 구현된 로봇이 해당 추상화 수준에서 정의된 의도를 충족한다는 것을 보여주는 증거와 연결된다.

가장 높은 개발 수준에서는 이해관계자(Stakeholder)가 로봇의 의도된 임무, 운용 환경, 사용자, 제약조건 및 허용 가능한 동작을 정의한다. 요구사항은 내비게이션(Navigation) 능력, 조작(Manipulation) 성능, 비행 동작, 인간 상호작용(Human Interaction), 가용성(Availability), 안전(Safety) 또는 환경적 한계를 설명할 수 있다. 모호한 운용 기대사항은 로봇 제작 이후 객관적으로 검증하기 어렵기 때문에 이러한 요구사항은 이후 인수 테스트(Acceptance Testing)를 지원할 수 있을 정도로 측정 가능해야 한다.

시스템 요구사항(System Requirements)은 운용 기대사항을 완전한 로봇이 제공해야 하는 기술적 동작으로 변환한다. 여기에서는 소프트웨어, 컴퓨팅 하드웨어(Computing Hardware), 센서(Sensor), 액추에이터(Actuator), 통신 네트워크(Communication Network), 안전 시스템(Safety System), 외부 인프라(External Infrastructure) 사이의 인터페이스를 정의한다. 위치 정확도, 응답 시간, 정지 거리, 제어 주파수, 추론 지연시간(Inference Latency), 임무 지속시간 또는 장애 복구 동작과 같은 성능 한계는 명확한 조건과 측정 가능한 합격 기준(Acceptance Criteria)으로 표현해야 한다.

시스템 아키텍처(System Architecture)는 이러한 요구사항을 상호작용하는 하위 시스템(Subsystem)으로 분해한다. 이동 로봇(Mobile Robot)은 인지(Perception), 위치추정(Localization), 매핑(Mapping), 계획(Planning), 제어(Control), 진단(Diagnostics), 안전, 데이터 로깅(Data Logging), 플릿 통신(Fleet Communication) 기능을 포함할 수 있다. 휴머노이드(Humanoid)나 매니퓰레이터(Manipulator)는 추가적인 모션(Motion), 힘(Force), 파지(Grasping), 전신 협응(Whole-Body Coordination) 기능을 요구하며, 무인항공기(UAV)는 비행 제어, 항법, 이중화(Redundancy), 임무 관리(Mission Management) 구성요소를 추가한다. 각각의 아키텍처 경계는 이후 테스트해야 할 인터페이스를 생성한다.

소프트웨어 아키텍처(Software Architecture)는 시스템 설계를 프로세스(Process), 서비스(Service), ROS 2 노드(Node), 라이브러리(Library), API, 데이터 파이프라인(Data Pipeline), 상태 머신(State Machine), 배포 단위(Deployment Unit)로 구체화한다. 엔지니어는 메시지 스키마(Message Schema), 좌표 프레임(Coordinate Frame), 타이밍 관계, 서비스 품질(QoS) 정책, 수명주기 상태(Lifecycle State), 오류 처리(Error Handling), 연산 자원 할당 및 하드웨어 추상화 경계(Hardware Abstraction Boundary)를 정의한다. 아키텍처 결정에 따라 통합 테스트와 계측(Instrumentation)이 필요한 상호작용이 결정되므로 검증 계획은 구현 이후가 아니라 이 단계부터 시작해야 한다.

상세 소프트웨어 설계(Detailed Software Design)는 구성요소를 알고리즘(Algorithm), 클래스(Class), 함수(Function), 상태 전이(State Transition), 데이터 구조(Data Structure), 구성 매개변수(Configuration Parameter), 내부 인터페이스로 더욱 세분화한다. 이 수준에서는 테스트 가능성(Testability)이 설계 자체의 속성이 된다. 결정론적 연산(Deterministic Computation)은 하드웨어 의존성과 분리되어야 하며, 필요한 경우 센서 접근을 추상화하고 예상 동작을 입력, 출력, 불변조건(Invariant), 허용오차(Tolerance), 실패 조건으로 표현하여 자동으로 검사할 수 있어야 한다.

구현(Implementation)은 V의 가장 아래쪽에 위치하며 상세 설계가 실행 가능한 소프트웨어와 구성으로 변환되는 단계이다. 소스 코드(Source Code), AI 추론 래퍼(AI Inference Wrapper), 제어기 구현, 장치 인터페이스(Device Interface), 실행 구성(Launch Configuration) 및 관련 자산은 원래의 요구사항과 설계 결정까지 추적 가능해야 한다. 정적 분석(Static Analysis), 코드 리뷰(Code Review), 빌드 검사(Build Check), 코딩 규칙 적용 및 개발자 로컬 테스트(Local Developer Test)는 구성요소가 공식 통합 단계로 진입하기 전에 초기 검증 증거를 제공한다.

V의 상승 측은 단위 테스트(Unit Testing)에서 시작하며 개별 소프트웨어 요소가 상세 설계의 기대사항을 만족하는지 검증한다. 수학 함수, 제어기 방정식, 변환(Transformation), 필터(Filter), 파서(Parser), 상태 머신, 안전 판정 조건(Safety Predicate), 유틸리티 라이브러리(Utility Library)를 결정론적 입력과 예상 출력으로 검사할 수 있다. 하드웨어 의존성은 일반적으로 모의 객체(Mock) 또는 스텁(Stub)으로 대체하여 실패를 국소화하고 개발 및 지속적 통합(Continuous Integration, CI) 과정에서 테스트를 신속하게 실행할 수 있도록 한다.

소프트웨어 통합 테스트(Software Integration Testing)는 소프트웨어 아키텍처 설계와 밀접하게 대응한다. 독립적으로 동작하는 구성요소를 결합한 후 실제에 가까운 통신 및 타이밍 조건에서 인터페이스를 검사한다. ROS 2 시스템에서는 토픽(Topic), 서비스, 액션(Action), 수명주기 전이(Lifecycle Transition), 네임스페이스(Namespace), QoS 호환성, 타임스탬프(Timestamp), 변환 트리(Transform Tree), 노드 시작 순서 등을 포함할 수 있다. API 계약(API Contract), 데이터베이스 인터페이스, 데이터 파이프라인 및 외부 미들웨어(External Middleware)에도 유사한 검증이 필요할 수 있다.

시스템 통합 테스트(System Integration Testing)는 소프트웨어와 물리적 또는 시뮬레이션된 하드웨어가 시스템 아키텍처에 따라 협력하는지를 평가한다. 센서, 액추에이터, 모터 제어기(Motor Controller), 임베디드 컴퓨터(Embedded Computer), 네트워크, 안전 장치(Safety Device), AI 가속기(AI Accelerator)를 점진적으로 테스트 구성에 포함할 수 있다. 시뮬레이션(Simulation)과 하드웨어 인 더 루프(Hardware-in-the-Loop, HIL) 환경은 완전한 물리적 로봇에서 잠재적으로 위험한 테스트를 수행하기 전에 실제적인 타이밍, 인터페이스 및 장애 조건을 검사할 수 있기 때문에 이 단계에서 특히 유용하다.

시스템 검증(System Verification)은 통합된 로봇이 명시된 기술적 요구사항을 만족하는지를 판단한다. 테스트는 요구사항 식별자(Requirement Identifier)와 직접 연결되어야 하며 객관적인 합격/불합격(Pass/Fail) 증거를 생성해야 한다. 내비게이션 정확도, 궤적 추종(Trajectory Tracking), 조작 정밀도, 제어 지연시간(Control Latency), 통신 동작, 비상 정지(Emergency Stop), 성능 저하 모드(Degraded-Mode) 동작, 자원 소비(Resource Consumption), 주입된 장애(Injected Fault)로부터의 복구 등이 사전에 정의된 정량적 한계에 대해 검증할 수 있는 대표적인 특성이다.

유효성 확인(Validation)은 의도된 사용 목적이라는 더 높은 수준에서 수행되며, 개발된 로봇이 실제 임무와 운용 환경에 적합한지를 판단한다. 기술적으로 올바른 내비게이션 스택(Navigation Stack)도 혼잡한 창고에서는 적합하지 않을 수 있으며, 실험실에서 높은 성공률을 보인 조작 정책(Manipulation Policy)도 실제 객체의 다양성에 직면하면 실패할 수 있다. 따라서 유효성 확인에는 내부적인 소프트웨어 정확성뿐만 아니라 대표적인 시나리오, 환경 조건, 운영자, 작업 흐름 및 성능 기대사항이 필요하다.

현장 테스트(Field Testing)는 실제 환경이 실험실 환경에서 완전히 재현할 수 없는 불확실성의 조합을 발생시키기 때문에 중요한 유효성 확인 증거를 제공한다. 조명, 지형, 진동, 온도, 무선 연결(Wireless Connectivity), 인간 행동, 객체 다양성, 날씨 및 장시간 운용은 새로운 형태의 복합적 장애(Emergent Failure)를 드러낼 수 있다. 현장 테스트 절차는 운용 요구사항에 대한 추적성을 유지하면서 소프트웨어 버전, 구성, 하드웨어 상태, 시나리오 조건, 텔레메트리(Telemetry) 및 관찰 결과를 기록해야 한다.

추적성(Traceability)은 V-모델의 양쪽을 연결하는 핵심 메커니즘이다. 요구사항 추적성 매트릭스(Requirements Traceability Matrix)는 이해관계자 요구, 시스템 요구사항, 아키텍처 구성요소, 상세 설계, 구현 산출물, 테스트 케이스(Test Case), 테스트 결과, 결함(Defect), 인수 증거(Acceptance Evidence)를 서로 연결할 수 있다. 양방향 추적성(Bidirectional Traceability)을 적용하면 테스트가 없는 요구사항, 정당한 요구사항과 연결되지 않은 테스트, 그리고 검증 영향이 아직 평가되지 않은 소프트웨어 변경사항을 식별할 수 있다.

V-모델을 반드시 순차적인 개발 프로세스(Sequential Development Process)로 해석할 필요는 없다. 현대적인 로봇 개발 프로그램은 반복적 개발(Iterative Development), 애자일(Agile), 데브옵스(DevOps), 지속적 통합(Continuous Integration) 워크플로 안에서도 V-모델을 적용할 수 있다. 요구사항, 아키텍처, 구현 및 테스트는 짧은 반복 주기 안에서 함께 발전하면서도 명세(Specification)와 증거(Evidence) 사이의 기본 관계를 유지할 수 있다. 자동화된 단위, 통합, 시뮬레이션 및 회귀 테스트(Regression Test)는 각 반복 과정에서 검증 체인의 일부를 지속적으로 재구축할 수 있도록 한다.

AI 기반 로봇(AI-Enabled Robot)의 경우 V-모델은 결정론적인 입력-출력 규칙만으로 성능을 완전히 명세하기 어려운 학습 기반 동작(Learned Behavior)도 수용해야 한다. 데이터셋 요구사항(Dataset Requirement), 모델 가정(Model Assumption), 학습 구성(Training Configuration), 시나리오 분포(Scenario Distribution), 강건성 기준(Robustness Criteria), 운용 경계(Operational Boundary)가 추가적인 개발 산출물이 된다. 이에 대응하는 평가 활동에는 오프라인 지표(Offline Metric), 시뮬레이션 시나리오, 분포 외 테스트(Out-of-Distribution Testing, OOD Testing), 실제 환경 시험(Real-World Trial), 성능 저하 모니터링(Performance Degradation Monitoring)이 포함된다.

따라서 로보틱스에서 V-모델의 핵심 가치는 설계되는 대상과 테스트되는 대상 사이에 체계적인 정렬(Alignment)을 구축하는 데 있다. 이를 통해 검증이 구현이 끝난 이후 별도로 수행되는 활동이 되는 것을 방지하고, 요구사항과 아키텍처가 정의되는 단계부터 테스트 계획을 수립하도록 한다. 단위 테스트, 통합 테스트, 시스템 테스트, 시뮬레이션, 하드웨어 인 더 루프(HIL), 현장 테스트와 결합하면 운용 의도(Operational Intent)에서부터 로봇이 요구된 방식으로 동작한다는 측정 가능한 증거에 이르기까지 추적 가능한 경로를 구축할 수 있다.

## 01.03. Test Driven Development TDD for Robot SW [w/Code]

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

테스트 주도 개발(Test-Driven Development, TDD)은 구현 코드(Production Code)를 작성하기 전에 해당 코드가 충족해야 할 자동화 테스트(Automated Test)를 먼저 작성하는 소프트웨어 엔지니어링(Software Engineering) 방식이다. 로봇 소프트웨어(Robot Software)에서는 알고리즘을 먼저 구현하고 나중에 테스트하는 일반적인 순서를 반대로 적용한다. 예상 동작, 인터페이스(Interface), 허용오차(Tolerance), 실패 조건을 조기에 명시함으로써 테스트 가능성(Testability)을 최종 품질관리 활동이 아니라 소프트웨어 설계 자체의 일부로 만든다.

TDD의 기본 주기는 일반적으로 레드(Red), 그린(Green), 리팩터(Refactor)로 설명된다. 레드 단계에서는 아직 존재하지 않는 동작을 설명하는 작은 테스트를 작성하고 예상한 이유로 테스트가 실패하는지 확인한다. 그린 단계에서는 해당 테스트를 통과하는 데 필요한 최소한의 구현만 추가한다. 리팩터 단계에서는 외부에서 관찰 가능한 동작을 변경하지 않으면서 코드 구조를 개선하고, 기존 테스트를 지속적으로 실행하여 기능이 그대로 유지되는지 검증한다.

레드(Red) 단계는 한 번도 실패하는 모습을 확인하지 않은 테스트가 잘못된 신뢰를 제공할 수 있기 때문에 특히 중요하다. 예를 들어 로봇 개발자가 속도 제한기(Velocity Limiter)를 구현한다면 허용 범위 내부와 외부의 명령에 대해 예상되는 출력을 먼저 정의할 수 있다. 구현 전에 테스트를 실행함으로써 해당 테스트가 아직 구현되지 않은 동작을 실제로 탐지하는지 확인한다. 동일한 방법을 좌표 변환, 궤적 제약조건(Trajectory Constraint), 센서 검증, 상태 전이(State Transition), 안전 판정 조건(Safety Predicate)에도 적용할 수 있다.

그린(Green) 단계에서는 현재의 동작 요구사항을 만족시키는 가장 작은 구현을 우선한다. 이러한 원칙은 불필요하게 이른 복잡성(Premature Complexity)을 억제하고 관찰 가능한 요구사항에 개발을 집중하도록 한다. 예를 들어 제어기 유틸리티(Controller Utility)는 처음에는 명확하게 정의된 하나의 운용 조건만 지원하고, 이후 새로운 테스트를 통해 포화(Saturation), 잘못된 입력, 타이밍 제약조건 또는 경계 조건(Boundary Condition)을 추가할 수 있다. 따라서 새로운 동작은 올바른 동작의 의미를 정의하는 실행 가능한 증거와 함께 도입된다.

충분히 강력한 자동화 테스트 스위트(Automated Test Suite)가 기존 동작을 보호하면 리팩터링(Refactoring)을 더욱 안전하게 수행할 수 있다. 로봇 소프트웨어는 알고리즘 최적화, 하드웨어 인터페이스 변경, 미들웨어(Middleware) 구성요소 재구성 또는 임베디드(Embedded), 엣지(Edge), 클라우드(Cloud) 자원 사이의 연산 작업 이동에 따라 지속적으로 변화한다. TDD는 내부 구현을 변경하면서도 테스트를 통해 인터페이스 계약(Interface Contract)과 동작 불변조건(Behavioral Invariant)을 유지하여 아키텍처 개선 과정에서 발견되지 않은 회귀(Regression)가 발생할 가능성을 줄인다.

TDD는 결정론적인 로봇 소프트웨어(Deterministic Robot Software)에 가장 직접적으로 적용할 수 있다. 수학 유틸리티, 운동학(Kinematics), 기하학(Geometry), 필터(Filter), 파서(Parser), 구성 검증기(Configuration Validator), 명령 제한기, 상태 머신(State Machine), 통제된 입력을 사용하는 플래너(Planner), 제어기 계산 등은 실제 하드웨어 없이도 테스트할 수 있다. 개발자는 알려진 입력을 제공하고 결과를 예상값 또는 허용오차와 비교함으로써 개발 장비와 지속적 통합(Continuous Integration, CI) 인프라에서 많은 테스트를 빠르게 실행할 수 있다.

수치 기반 로보틱스 알고리즘(Numerical Robotics Algorithm)은 부동소수점(Floating-Point) 결과를 정확한 동등성으로 비교하는 것이 적절하지 않은 경우가 많기 때문에 세심한 단언(Assertion)이 필요하다. 테스트에서는 알고리즘과 시스템 요구사항에서 도출된 의미 있는 절대 또는 상대 허용오차를 정의해야 한다. 변환 행렬(Transformation Matrix)은 예상 자세 관계, 역변환 일관성(Inverse Consistency), 정규화 특성을 검사할 수 있으며, 궤적 계산은 경계 조건, 연속성, 속도 제한, 가속도 제약조건 및 물리적으로 유효하지 않은 입력을 대상으로 테스트할 수 있다.

하드웨어 의존성(Hardware Dependency)은 일반적인 TDD가 빠르고 반복 가능하며 격리된 실행을 전제로 하기 때문에 중요한 과제가 된다. 카메라(Camera), 라이다(LiDAR), 관성측정장치(Inertial Measurement Unit, IMU), 모터 드라이버(Motor Driver), 위성항법시스템(GNSS) 수신기 또는 로봇 버스(Robot Bus)에 직접 접근하면 테스트가 느려지고 비결정적(Nondeterministic)이 될 수 있다. 하드웨어 추상화 계층(Hardware Abstraction Layer)과 의존성 주입(Dependency Injection)을 사용하면 의사결정 로직을 장치 접근과 분리하고, 모의 객체(Mock), 스텁(Stub), 기록 데이터 또는 시뮬레이션 인터페이스를 통해 통제된 관측값을 제공하고 생성된 명령을 확인할 수 있다.

ROS 2 소프트웨어에서는 가능한 경우 노드 동작(Node Behavior)을 통신 인프라(Communication Infrastructure)와 분리함으로써 TDD를 적용할 수 있다. 핵심 계산과 의사결정 로직은 독립적으로 테스트 가능한 라이브러리에 배치하고, 얇은 ROS 2 어댑터(Adapter)가 토픽(Topic), 서비스(Service), 액션(Action), 매개변수(Parameter), 수명주기 전이(Lifecycle Transition), 변환(Transform)을 처리하도록 구성할 수 있다. 이후 단위 테스트는 결정론적 로직을 빠르게 검사하고, 별도의 통합 테스트(Integration Test)는 QoS 호환성, 메시지 흐름, 타임스탬프(Timestamp), 네임스페이스(Namespace), 노드 상호작용과 같은 미들웨어 동작을 검증한다.

제어기 개발(Controller Development)에서도 테스트를 통한 명세(Specification)의 이점을 활용할 수 있다. PID 제어기(PID Controller), 궤적 추종기(Trajectory Tracker), 보행 구성요소(Gait Component), 액추에이터 명령 처리기(Actuator Command Processor)를 구현하기 전에 정상 입력, 포화, 영 오차(Zero Error), 잘못된 매개변수, 극단값 및 상태 초기화(State Reset)에 대한 예상 응답을 정의할 수 있다. 이러한 테스트만으로 완전한 물리적 로봇의 폐루프 안정성(Closed-Loop Stability)을 입증할 수는 없지만 시뮬레이션, HIL 및 시스템 수준 검증 이전에 소프트웨어 구성요소의 신뢰할 수 있는 동작을 확립할 수 있다.

인지(Perception) 및 AI 구성요소에는 출력이 확률적일 수 있고 모델 성능을 하나의 결정론적인 단언으로 표현하기 어렵기 때문에 TDD를 변형하여 적용해야 한다. 그럼에도 테스트를 통해 전처리 차원(Preprocessing Dimension), 텐서 유형(Tensor Type), 정규화(Normalization), 모델 로딩(Model Loading), 출력 스키마(Output Schema), 신뢰도 범위(Confidence Range), 지연시간 한계 및 실패 처리 동작을 정의할 수 있다. 이후 통계적 성능과 일반화(Generalization)를 평가하려면 데이터셋 수준 평가(Dataset-Level Evaluation)와 시나리오 기반 검증(Scenario-Based Validation)을 이러한 소프트웨어 테스트와 함께 수행해야 한다.

TDD에서는 구성요소 정확성(Component Correctness)과 완전한 로봇의 유효성 확인(Robot Validation)을 구분해야 한다. 단위 테스트를 통과했다고 해서 자율이동로봇(AMR)이 창고를 안전하게 주행하거나, 휴머노이드(Humanoid)가 물체를 조작하면서 균형을 유지하거나, 무인항공기(UAV)가 실제적인 외란(Disturbance)을 견딜 수 있다는 것이 입증되는 것은 아니다. 따라서 더 넓은 테스트 체계는 소프트웨어 단위 및 통합 테스트에서 HIL, 시뮬레이션 기반 검증, 현장 테스트(Field Testing), AI 평가, 안전 테스트, 벤치마킹(Benchmarking), 인증(Certification) 활동으로 확장된다.

지속적 통합(Continuous Integration)은 커밋(Commit)된 모든 변경사항에 대해 소프트웨어를 자동으로 다시 빌드하고 누적된 회귀 테스트 스위트(Regression Test Suite)를 실행할 수 있기 때문에 TDD의 가치를 더욱 높인다. 개발 중 발견된 결함(Defect)은 먼저 문제를 재현하는 실패 테스트로 변환할 수 있다. 구현을 수정한 이후에도 해당 테스트를 테스트 스위트에 영구적으로 유지함으로써 특정 장애를 향후 동일한 동작이 조용히 재발하는 것을 방지하는 재사용 가능한 검증 증거로 전환할 수 있다.

테스트의 품질(Test Quality)은 단순히 테스트 개수를 증가시키는 것보다 중요하다. 테스트는 이해하기 쉽고, 결정론적이며, 서로 독립적이고, 의도된 실행 빈도에 적합할 정도로 빠르며, 검증 대상 동작을 명확하게 표현해야 한다. 내부 구현 세부사항에 지나치게 의존하면 테스트가 취약해져 기능에 영향을 주지 않는 리팩터링만으로도 테스트 스위트가 실패할 수 있다. 따라서 좋은 TDD는 외부적으로 의미 있는 동작과 안정적인 계약(Stable Contract)을 강조하면서 테스트와 비공개 구현 구조 사이의 불필요한 결합(Coupling)을 피한다.

안전 관련 로봇 소프트웨어(Safety-Related Robot Software)는 추가적인 엄격성이 요구된다. TDD를 사용하여 명령 제한, 감시 타이머(Watchdog), 상태 전이, 타당성 검사(Plausibility Check), 장애 대응(Fault Response), 안전 관련 소프트웨어 로직의 예상 동작을 코드화할 수 있지만, TDD만으로 기능 안전(Functional Safety) 적합성을 입증할 수는 없다. 안전 요구사항에는 추적성(Traceability), 적절한 검증 엄격성, 필요한 경우 검증 독립성(Verification Independence), 장애 주입 테스트(Fault-Injection Testing), 시스템 수준 증거 및 일반적인 개발자 중심 TDD 작업 흐름을 넘어서는 인증 활동이 필요하다.

실용적인 로봇 소프트웨어 조직에서는 TDD를 테스트 피라미드(Testing Pyramid)와 V-모델(V-Model)을 대체하는 방법으로 사용하지 않고 이들과 결합한다. TDD는 구현과 가까운 위치에서 실행 가능한 명세(Executable Specification)를 생성함으로써 테스트 피라미드의 하위 계층을 강화하며, 통합, 시스템, 시뮬레이션, HIL 및 현장 테스트는 상호작용과 물리적 동작을 점진적으로 평가한다. 요구사항 추적성(Requirements Traceability)은 이러한 계층을 연결하여 개발자 테스트가 더 큰 검증 및 유효성 확인 증거 체인(Verification and Validation Evidence Chain)의 일부가 되도록 한다.

TDD의 장기적인 이점은 단순히 더 많은 테스트를 확보하는 것이 아니라 구현이 복잡해지기 전에 소프트웨어 동작을 지속적으로 명세하고 검증하는 개발 문화(Development Culture)를 구축하는 데 있다. 알고리즘, 미들웨어, 하드웨어, AI 모델(AI Model), 물리적 환경 사이의 상호작용에서 장애가 자주 발생하는 로보틱스 분야에서 이러한 원칙은 신뢰할 수 있는 소프트웨어 기반을 형성하며, 이를 바탕으로 점진적으로 더 현실적인 검증 및 유효성 확인(Verification and Validation)을 수행할 수 있다.

## 01.04. Behavior Driven Development BDD Gherkin [w/Code]

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

행동 주도 개발(Behavior-Driven Development, BDD)은 개발자, 테스터(Tester), 도메인 전문가(Domain Expert) 및 기타 이해관계자가 모두 이해할 수 있는 언어로 시스템의 예상 동작을 표현하는 협업형 소프트웨어 개발 접근법이다. 로봇 소프트웨어(Robot Software)에서 BDD는 내부 구현 세부사항에 집중하기보다 특정 조건에서 로봇이 무엇을 수행해야 하는지를 설명함으로써 운용 의도(Operational Intention)를 실행 가능한 테스트(Executable Test)와 연결한다. 이를 통해 동작(Behavior)은 여러 분야가 공유하는 엔지니어링 계약(Engineering Contract)이 된다.

BDD는 개별 함수보다 외부적으로 의미 있는 동작에 초점을 이동시킴으로써 테스트 주도 개발(Test-Driven Development, TDD)을 보완한다. TDD가 속도 제한 함수(Velocity-Limiting Function)가 올바른 수치 값을 반환하는지를 검증한다면, BDD는 자율이동로봇(Mobile Robot)이 제한 구역(Restricted Zone)에 진입할 때 속도를 감소시켜야 한다는 동작을 명세할 수 있다. 두 접근법 모두 자동화 검증(Automated Verification)을 지원하지만 BDD는 소프트웨어 기능이 관찰 가능한 로봇 동작에 어떻게 기여하는지를 설명하는 시나리오(Scenario)를 강조한다.

거킨(Gherkin)은 BDD 시나리오를 읽을 수 있고 실행 가능한 형태로 표현하는 데 일반적으로 사용되는 구조화 언어(Structured Language)이다. 핵심 어휘에는 기능(Feature), 시나리오(Scenario), 주어진 조건(Given), 이벤트 또는 행동(When), 예상 결과(Then), 추가 조건(And) 및 관련 구문이 포함된다. 기능은 명세하려는 능력을 나타내고 각각의 시나리오는 하나의 구체적인 동작 사례를 설명한다. 이러한 어휘는 소스 코드(Source Code)를 직접 확인할 필요가 없는 사람도 이해할 수 있으면서 자동화에 필요한 충분한 구조를 제공한다.

주어진 조건-이벤트-예상 결과(Given-When-Then) 패턴은 핵심적인 동작 구조를 제공한다. 주어진 조건(Given)은 초기 상황과 관련 사전조건(Precondition)을 설정하고, 이벤트 또는 행동(When)은 발생하는 사건이나 동작을 설명하며, 예상 결과(Then)는 외부에서 관찰할 수 있는 결과를 정의한다. 예를 들어 초기 상황에서 자율이동로봇(Autonomous Mobile Robot)이 정상적으로 주행하고 있다고 설정하고, 이벤트 단계에서 진행 경로에 장애물을 추가하며, 예상 결과에서는 정의된 안전 동작에 따라 로봇이 감속하거나 정지하도록 요구할 수 있다.

좋은 BDD 시나리오는 구현 메커니즘(Implementation Mechanism)이 아니라 동작을 설명한다. 일반적으로 시나리오는 비공개 메서드(Private Method)나 내부 클래스 구조를 지정하기보다 로봇이 목적지에 도달하고, 안전하지 않은 명령을 거부하고, 안전 상태(Safe State)로 전환하거나, 감지된 장애를 보고해야 한다고 표현해야 한다. 이러한 분리를 통해 외부에서 요구되는 동작이 유지되는 한 동작 명세를 불필요하게 다시 작성하지 않고도 알고리즘과 아키텍처를 리팩터링(Refactoring)할 수 있다.

BDD는 로보틱스 요구사항(Robotics Requirement)에 소프트웨어, 시스템, 안전 및 운영팀이 공유하는 용어가 포함되어 있을 때 특히 유용하다. 안전 정지(Safe Stop), 도킹 완료(Docking Complete), 위치추정 상실(Localization Lost), 임무 중단(Mission Aborted), 운영자 제어 전환(Operator Takeover), 장애물 감지(Obstacle Detected) 등의 표현에 정확한 운용 의미를 부여할 수 있다. 시나리오를 공동으로 검토하면 구현 전에 모호한 요구사항을 발견하고 조건, 이벤트, 결과, 허용오차 및 예외 동작(Exceptional Behavior)에 대해 이해관계자가 합의하도록 할 수 있다.

로봇 소프트웨어의 시나리오 설계(Scenario Design)에서는 물리량(Physical Quantity)과 허용오차(Tolerance)를 고려해야 한다. 로봇이 "안전하게 정지한다"는 표현만으로는 충분하지 않으며 프로젝트에서 최대 정지거리(Maximum Stopping Distance), 속도 임계값(Velocity Threshold), 응답시간(Response Time) 또는 보호구역 경계(Protected-Zone Boundary)와 같은 측정 가능한 조건을 정의해야 한다. Gherkin 시나리오는 읽기 쉬운 도메인 언어(Domain Language)를 유지하면서 단계 구현(Step Implementation)을 통해 이러한 표현을 텔레메트리(Telemetry), 상태 변수, 메시지 또는 기록된 측정값에 대한 정량적 단언(Quantitative Assertion)으로 변환할 수 있다.

ROS 2 시스템에는 BDD 자동화에 적합한 관찰 가능한 경계가 많이 존재한다. 시나리오 단계에서는 노드 수명주기 상태(Node Lifecycle State)를 설정하고, 센서 관측값을 발행하며, 매개변수(Parameter)를 구성하고, 서비스 요청(Service Request)이나 액션(Action)을 실행한 다음 토픽(Topic), 변환(Transform), 진단 상태(Diagnostic State) 또는 생성된 명령을 검증할 수 있다. 동작 명세는 불필요한 미들웨어(Middleware) 세부사항으로부터 독립적으로 유지하고, 내부 단계 정의가 시나리오 실행에 필요한 기술적 상호작용을 수행하도록 해야 한다.

내비게이션 소프트웨어(Navigation Software)에서는 BDD 시나리오를 통해 경로 차단, 위치추정 성능 저하, 목표 취소, 제한 구역, 도킹 실패 또는 동적 장애물(Dynamic Obstacle)과 같은 운용 상황을 표현할 수 있다. 하나의 시나리오에서 유효한 지도와 위치가 추정된 로봇을 초기 상태로 설정하고, 주행 중 장애물을 추가한 다음, 로봇이 안전거리를 유지하면서 목표에 도달하거나 정의된 복구 상태(Recovery State)로 전환하도록 요구할 수 있다. 이러한 시나리오는 요구사항과 종단간 통합 테스트(End-to-End Integration Testing)를 연결한다.

조작 시스템(Manipulation System)에서도 객체 획득(Object Acquisition), 파지 실패(Grasp Failure), 힘 제한(Force Limit), 작업공간 제약조건(Workspace Constraint), 복구(Recovery)와 관련된 동작을 유사한 방식으로 설명할 수 있다. 파지 계획기(Grasp Planner)의 수학적 출력만 테스트하는 대신, 객체에 도달할 수 없거나 측정된 힘이 허용 임계값을 초과하면 로봇이 현재 동작을 중단하고 안전하지 않은 액추에이터 명령(Actuator Command)을 발생시키지 않으면서 적절한 복구 상태로 전환해야 한다는 BDD 시나리오를 정의할 수 있다.

휴머노이드(Humanoid)와 다족보행로봇(Legged Robot)의 경우 시나리오는 균형 복구(Balance Recovery), 지형 전환(Terrain Transition), 접촉 변화(Contact Change), 운영자 상호작용 또는 작업 중단을 표현할 수 있다. 무인항공기(UAV)에서는 통신 상실, 항법 성능 저하, 임무 취소, 지오펜스(Geofence) 상호작용 또는 비상 동작(Emergency Behavior)을 설명할 수 있다. 따라서 동일한 BDD 구조를 사용하면서도 로봇 조직 전체에서 일관된 명세 방식을 유지하고 플랫폼별 운용 동작을 표현할 수 있다.

BDD는 AI 기반 로봇 기능(AI-Enabled Robot Function)에도 적용할 수 있지만 확률적 동작(Probabilistic Behavior)을 신중하게 다루어야 한다. 결정성이 보장되지 않는 상황에서 모든 모델 추론(Model Inference)이 동일한 결과를 생성한다고 가정해서는 안 된다. 대신 BDD를 사용하여 모델 출력, 신뢰도 조건(Confidence Condition), 유효하지 않은 관측값, 사용 불가능한 모델 또는 운용 경계에 대한 시스템 수준의 대응을 검증하고, 통계적 모델 품질은 데이터셋(Dataset)과 별도의 AI 평가 프로토콜(AI Evaluation Protocol)을 통해 평가할 수 있다.

시나리오 개요(Scenario Outline)와 매개변수화된 예제(Parameterized Example)는 동일한 동작을 여러 조건에서 평가해야 할 때 유용하다. 여러 속도 제한, 장애물 거리, 페이로드 상태(Payload State) 또는 운용 모드(Operating Mode)에 대해 거의 동일한 시나리오를 반복 작성하는 대신 하나의 공통 동작 구조에 서로 다른 값을 적용하여 실행할 수 있다. 이를 통해 명세의 가독성을 유지하면서 커버리지(Coverage)를 높일 수 있지만, 지나친 매개변수화는 이해관계자가 시나리오를 이해하기 어렵게 만들 수 있으므로 적절하게 통제해야 한다.

단계 정의(Step Definition)는 읽기 쉬운 Gherkin 문장을 실행 가능한 테스트 코드와 연결하는 자동화 계층(Automation Layer)을 형성한다. 단계 정의는 API를 호출하고, ROS 2 메시지를 발행하고, 시뮬레이션 환경(Simulated Environment)을 조작하고, 텔레메트리를 검사하고, 상태 머신(State Machine)을 조회하거나 기록된 출력을 평가할 수 있다. 잘못 설계된 단계 라이브러리(Step Library)는 자동화 로직의 중복을 발생시키고 로봇 아키텍처가 발전하면서 동작 명세를 유지하기 어렵게 만들 수 있으므로 단계 구현은 재사용 가능하고 안정적이어야 한다.

BDD 시나리오는 테스트 피라미드(Testing Pyramid)의 여러 수준에서 실행할 수 있다. 경량 시나리오는 모의 객체(Mock)를 사용하여 소프트웨어 구성요소를 검사할 수 있으며, 통합 시나리오는 여러 ROS 2 노드를 실행하고 시스템 시나리오는 시뮬레이션 또는 하드웨어 인 더 루프(Hardware-in-the-Loop, HIL) 환경을 대상으로 동작할 수 있다. 비용이 높은 일부 동작 시나리오는 통제된 현장 테스트(Field Test) 절차로 확장될 수도 있다. 따라서 로봇 검증은 소프트웨어 통합, HIL, 시뮬레이션 및 현장 테스트를 통해 점진적으로 확장될 수 있다.

지속적 통합(Continuous Integration, CI)을 활용하면 실행 가능한 BDD 시나리오를 회귀 테스트(Regression Test)로 사용할 수 있다. 요구사항이나 결함(Defect)이 하나의 시나리오로 변환되면 관련 소프트웨어가 변경될 때마다 해당 시나리오를 자동으로 실행할 수 있다. 테스트 실패는 단순히 코드가 손상되었다는 사실뿐만 아니라 어떤 예상 동작이 더 이상 충족되지 않는지를 보여준다. 이러한 동작 중심 보고(Behavioral Reporting)는 낮은 수준의 테스트 실패 정보만 제공하는 것보다 다분야 팀(Multidisciplinary Team)에 더 유용한 정보를 제공할 수 있다.

BDD 시나리오를 요구사항, 위험요소(Hazard), 사용자 스토리(User Story) 또는 인수 기준(Acceptance Criteria)에 연결하면 추적성(Traceability)도 향상된다. 안전 또는 운용 요구사항을 정상 및 비정상 조건에서 예상되는 동작을 입증하는 하나 이상의 시나리오와 연결할 수 있다. 이후 테스트 결과는 해당 요구사항과 실행 가능한 검증(Executable Verification)을 연결하는 증거를 제공한다. 이러한 관계는 상위 수준 명세와 이에 대응하는 유효성 확인 활동(Validation Activity)의 연결을 강화함으로써 V-모델(V-Model)을 보완한다.

BDD는 단위 테스트(Unit Testing), 통계적 AI 평가(Statistical AI Evaluation), 시뮬레이션 캠페인(Simulation Campaign), HIL 테스트, 안전 분석(Safety Analysis) 또는 현장 유효성 확인(Field Validation)을 대체해서는 안 된다. 동작 시나리오는 예상되는 시스템 동작의 선택된 사례를 설명하는 것이며 모든 물리적 상호작용이나 환경적 불확실성을 완전하게 표현할 수는 없다. BDD의 가장 중요한 역할은 로봇 개발 수명주기 전반에서 이해관계자의 의도, 요구사항, 소프트웨어 구현 및 관찰 가능한 검증을 연결하는 공통의 실행 가능한 언어(Common Executable Language)를 구축하는 것이다.

따라서 성숙한 로보틱스 개발 워크플로(Robotics Development Workflow)는 BDD와 Gherkin을 TDD, 테스트 피라미드, 요구사항 추적성(Requirements Traceability), 지속적 테스트(Continuous Testing)와 결합한다. TDD는 세부적인 소프트웨어 동작을 보호하고, BDD는 팀이 구현 전에 논의하고 구현 이후 실행할 수 있는 의미 있는 운용 사례를 표현한다. 두 접근법을 함께 적용하면 정적인 요구사항 문서를 점차 정밀하고 테스트 가능한 엔지니어링 증거(Engineering Evidence)로 변환하여 로봇이 의도된 동작과 실제 소프트웨어가 수행하는 동작 사이의 모호성을 줄일 수 있다.

## 01.05. Test Coverage Metrics Line Branch MC DC [w/Code]

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

테스트 커버리지 지표(Test Coverage Metrics)는 테스트 스위트(Test Suite)가 소프트웨어 구현의 어느 부분을 실행했는지에 대한 정량적 증거를 제공한다. 로봇 소프트웨어(Robot Software)에서는 제어(Control), 인지(Perception), 계획(Planning), 안전(Safety), 통신(Communication), 하드웨어 인터페이스(Hardware Interface) 구성요소에 많은 조건부 실행 경로가 존재하므로 커버리지 분석(Coverage Analysis)이 특히 중요하다. 커버리지는 정확성을 증명하지는 않지만 테스트 과정에서 거의 또는 전혀 실행되지 않은 구현 영역을 식별하는 데 도움을 준다.

라인 커버리지(Line Coverage)는 실행 가능한 소스 코드(Source Code)의 각 라인이 하나 이상의 테스트에 의해 실행되었는지를 측정한다. 하나의 모듈(Module)에 실행 가능한 코드 100줄이 있고 테스트가 그중 90줄을 실행했다면 라인 커버리지는 약 90%이다. 이 지표는 이해하기 쉽고 전혀 테스트되지 않은 함수나 코드 블록을 식별하는 데 유용하므로 단위 테스트(Unit Testing)와 지속적 통합(Continuous Integration, CI) 파이프라인에서 실용적인 기준 지표로 사용할 수 있다.

높은 라인 커버리지만으로는 하나의 코드 라인을 실행했다는 사실이 해당 라인에 영향을 주는 모든 의사결정(Decision)을 평가했다는 것을 의미하지 않기 때문에 잘못된 신뢰를 제공할 수 있다. 조건문(Conditional Statement)이 반복적으로 실행되더라도 항상 동일한 결과만 선택될 수 있다. 로봇 소프트웨어에는 유효하거나 잘못된 센서 데이터, 통신 장애, 성능 저하 상태(Degraded State), 액추에이터 제한(Actuator Limit), 안전 대응 등을 처리하는 로직이 많으므로 단순한 실행 횟수를 넘어 의사결정 동작을 검사해야 한다.

브랜치 커버리지(Branch Coverage)는 제어 흐름(Control Flow)의 의사결정에서 발생할 수 있는 서로 다른 결과가 실행되었는지를 측정한다. 예를 들어 if-else 문에서는 일반적으로 참(True)과 거짓(False) 브랜치가 모두 테스트를 통해 실행되어야 한다. 동일한 원칙이 switch의 각 분기, 반복문 조건, 예외 경로(Exception Path), 복합 의사결정(Compound Decision)에도 적용된다. 따라서 브랜치 커버리지는 테스트가 소프트웨어 구성요소의 다양한 동작 경로를 탐색한다는 점에서 라인 커버리지보다 강한 증거를 제공한다.

예를 들어 로봇의 모션 명령(Motion Command)이 위치추정(Localization)이 유효하고 비상 정지(Emergency Stop)가 활성화되지 않은 경우에만 허용된다고 가정할 수 있다. 정상 운용만 검사하는 테스트는 관련 소스 라인을 실행하면서도 중요한 의사결정 결과를 검사하지 못할 수 있다. 브랜치 중심 테스트에서는 위치추정이 유효하지 않은 경우, 비상 정지가 활성화된 경우 및 기타 관련 조건을 추가하여 실제 물리적 시스템의 비정상 운용 상황이 발생하기 전까지 실행되지 않을 수 있는 로직을 검사한다.

조건 커버리지(Condition Coverage)는 하나의 복합 의사결정을 구성하는 개별 불리언 조건(Boolean Condition)을 검사한다. 의사결정이 위치추정 유효성, 장애물 안전거리(Obstacle Clearance), 통신 상태(Communication Health)에 의존한다면 테스트 과정에서 각각의 조건이 참과 거짓으로 평가되는 상황을 모두 확인해야 한다. 이는 최종 의사결정 결과만 관찰하는 것보다 더 상세한 증거를 제공하지만, 조건 커버리지만으로는 각각의 조건이 최종 결과에 독립적으로 영향을 미친다는 사실까지 반드시 입증되는 것은 아니다.

수정 조건/의사결정 커버리지(Modified Condition/Decision Coverage, MC/DC)는 각각의 개별 조건이 의사결정 결과에 독립적으로 영향을 미칠 수 있다는 증거를 요구함으로써 이러한 개념을 강화한다. 복합 불리언 표현식(Compound Boolean Expression)의 각 조건에 대해 관련된 다른 조건을 고정한 상태에서 해당 조건을 변경했을 때 전체 의사결정 결과도 변경된다는 것을 적절한 테스트 쌍(Test Pair)을 통해 입증한다. 이러한 특성으로 인해 MC/DC는 높은 무결성(High-Integrity)을 요구하는 소프트웨어의 복잡한 의사결정 로직에 특히 유용하다.

MC/DC는 모든 가능한 불리언 조합을 완전하게 평가하는 방식과 비교하여 테스트 수를 상당히 줄이면서도 조건 간의 의미 있는 독립성을 입증할 수 있다. 여러 개의 불리언 입력을 포함하는 의사결정은 이론적으로 매우 많은 조합을 생성할 수 있지만 MC/DC는 각 입력이 독립적으로 영향을 미친다는 것을 보여주는 신중하게 선택된 테스트 집합을 사용한다. 따라서 목적은 전체 진리표(Truth Table)를 무차별적으로 열거하는 것이 아니라 구조적인 검증 엄격성(Structural Rigor)을 확보하는 것이다.

로보틱스(Robotics)에서 MC/DC는 잘못된 의사결정 동작이 위험한 결과(Hazardous Outcome)에 기여할 가능성이 있는 소프트웨어에 특히 중요하다. 대표적인 예로 명령 승인(Command Authorization), 안전 상태 전이(Safety-State Transition), 액추에이터 활성화(Actuator Enabling), 장애 대응(Fault Reaction), 비행 모드 전환(Flight-Mode Transition), 모션 억제(Motion Inhibition), 성능 저하 운용(Degraded Operation) 로직 등이 있다. 이러한 구성요소에 더 강력한 커버리지 기준을 적용하면 일반적인 라인 또는 브랜치 커버리지로 충분히 검사하기 어려운 의도하지 않은 결합(Unintended Coupling), 가려진 조건(Masked Condition), 불리언 표현식의 문제를 발견하는 데 도움이 된다.

따라서 커버리지 목표(Coverage Target)는 전체 로봇 코드베이스(Codebase)에 하나의 비율을 일률적으로 적용하기보다 소프트웨어 중요도(Criticality)와 위험(Risk)에 따라 선정해야 한다. 시각화 유틸리티(Visualization Utility)와 안전 관련 모션 허가 모듈(Safety-Related Motion-Permission Module)이 반드시 동일한 수준의 구조적 증거를 요구하는 것은 아니다. 위험 기반 테스트(Risk-Based Testing)를 적용하면 위험요소(Hazard)와 관련된 구성요소에는 더 강한 기준과 검토 요구사항을 부여하고 중요도가 낮은 지원 소프트웨어에는 비교적 단순한 커버리지 목표를 적용할 수 있다.

커버리지 분석에서는 도달 불가능 코드(Unreachable Code)와 방어적 코드(Defensive Code)도 의미 있게 다루어야 한다. 일부 브랜치는 하드웨어 장애, 손상된 메시지, 유효하지 않은 상태 또는 정상 실행에서는 재현하기 어려운 조건을 처리하기 위해 존재할 수 있다. 이러한 코드를 자동으로 제외하기보다 모의 객체(Mock), 장애 주입(Fault Injection), 시뮬레이션(Simulation), 하드웨어 인 더 루프(Hardware-in-the-Loop, HIL)를 통해 실행할 수 있는지를 판단해야 한다. 실제로 도달 불가능한 코드는 그 근거를 정당화하고 검토하며 문서화해야 한다.

생성 코드(Generated Code), 서드파티 라이브러리(Third-Party Library), 미들웨어 내부 코드(Middleware Internals), 플랫폼별 코드 영역(Platform-Specific Section)에 대해서도 명확한 커버리지 정책(Coverage Policy)이 필요하다. 개발팀이 외부 구현을 자체 소프트웨어와 동일한 방식으로 통제하거나 테스트할 수 없는 경우 모든 의존성을 측정하면 프로젝트 지표가 왜곡될 수 있다. 따라서 보고되는 비율을 해석하고 비교할 수 있도록 어떤 소스 파일, 생성 산출물, 어댑터(Adapter), 라이브러리 및 테스트 유틸리티를 측정 범위에 포함할 것인지 명확하게 정의해야 한다.

ROS 2 로봇 소프트웨어에서는 구조적 커버리지(Structural Coverage)와 인터페이스 중심 테스트(Interface-Oriented Testing)를 결합하는 것이 효과적이다. 핵심 라이브러리는 빠른 단위 테스트 중에 라인, 브랜치 및 조건 커버리지를 측정할 수 있으며, 통합 테스트(Integration Test)는 노드 통신(Node Communication), 서비스(Service), 액션(Action), 매개변수(Parameter), 수명주기 동작(Lifecycle Behavior), 변환(Transform)을 검사한다. 여러 테스트 단계에서 수집한 커버리지 데이터를 결합하면 통합 실행을 통해서만 도달하는 로직과 시스템 수준 시나리오를 수행했음에도 여전히 테스트되지 않은 로직을 식별할 수 있다.

제어기(Controller)와 수치 소프트웨어(Numerical Software)에서는 커버리지 지표를 경계값 테스트(Boundary-Value Testing) 및 수치 테스트(Numerical Testing)와 결합해야 한다. 포화 조건(Saturation Condition)의 양쪽 경로를 실행했다는 사실만으로 한계값 주변의 동작이 올바르다는 것을 입증할 수는 없다. 테스트는 중요한 임계값보다 작은 값, 임계값과 동일한 값, 임계값보다 큰 값을 검사하고 부동소수점 허용오차(Floating-Point Tolerance), 잘못된 값, 초기화 상태, 리셋 동작(Reset Behavior), 수치적 극단값(Numerical Extreme)을 고려해야 한다. 구조적 커버리지는 실행 경로를 식별하고 단언(Assertion)은 결과의 정확성을 검증한다.

AI 기반 로봇 소프트웨어(AI-Enabled Robot Software)에서는 소스 코드 커버리지가 학습 모델(Learned Model)의 동작 커버리지(Behavioral Coverage)를 측정하지 못한다는 또 다른 차이가 존재한다. 신경망 추론 래퍼(Neural Network Inference Wrapper)가 완전한 라인 커버리지를 달성하더라도 모델이 중요한 객체 클래스, 환경 조건 또는 분포 외 입력(Out-of-Distribution Input)을 경험하지 않았을 수 있다. 따라서 AI 평가에서는 기존의 소프트웨어 구조적 지표와 함께 데이터셋, 시나리오, 분포(Distribution), 강건성(Robustness), 작업 성능(Task Performance)에 대한 커버리지를 추가로 평가해야 한다.

커버리지 측정은 지속적 통합(Continuous Integration)에 포함할 때 가장 효과적으로 활용할 수 있다. 모든 소프트웨어 변경은 테스트 실행, 커버리지 정보 수집, 정의된 임계값과의 비교 및 새롭게 커버되지 않은 코드 식별을 자동으로 수행하도록 구성할 수 있다. 이를 통해 중요한 커버리지 저하(Coverage Regression)를 방지하면서 장기적인 변화 추세를 관리할 수 있다. 그러나 단순히 비율을 높이기 위한 피상적인 테스트를 작성해서는 안 된다. 의미 있는 단언이 없는 실행은 검증 가치가 동일하게 증가하지 않은 상태에서 커버리지 통계만 높일 수 있기 때문이다.

커버리지 보고서(Coverage Report)는 단순한 관리 점수(Management Score)가 아니라 엔지니어링 조사를 지원해야 한다. 엔지니어는 커버되지 않은 라인, 브랜치 및 의사결정을 확인하고 해당 영역이 테스트되지 않은 이유를 분석해야 한다. 그 결과 누락된 테스트, 사용되지 않는 코드(Obsolete Code), 테스트하기 어려운 아키텍처(Untestable Architecture), 부족한 장애 주입 또는 정당화되지 않은 방어적 실행 경로를 발견할 수 있다. 따라서 커버리지 분석은 테스트 완전성(Test Completeness)뿐만 아니라 소프트웨어 설계와 테스트 가능성에 대한 피드백도 제공한다.

커버리지는 궁극적으로 요구사항 추적성(Requirements Traceability), 테스트 품질(Test Quality), 위험 분석(Risk Analysis), 상위 수준 유효성 확인(Higher-Level Validation)과 함께 해석해야 한다. 구조적 커버리지가 100%라고 하더라도 요구사항이 완전하거나 알고리즘이 정확하고 타이밍이 적절하며 물리적 로봇이 실제 환경에서 안전하게 동작한다는 것을 입증할 수는 없다. 따라서 전체 테스트 체계는 소프트웨어 테스트를 넘어 HIL, 시뮬레이션, 현장 테스트(Field Testing), 안전 평가(Safety Evaluation), 벤치마킹(Benchmarking), 인증(Certification) 활동으로 확장된다.

성숙한 로보틱스 테스트 전략(Robotics Testing Strategy)은 라인, 브랜치, 조건 및 MC/DC 커버리지를 서로 대체 가능한 단순한 백분율이 아니라 점진적으로 강화되는 구조적 증거(Structural Evidence)로 취급한다. 라인 커버리지는 실행된 구현 영역을 식별하고, 브랜치 커버리지는 의사결정 결과를 검사하며, MC/DC는 중요한 의사결정 내부에서 개별 조건이 독립적으로 미치는 영향을 검증한다. 이러한 지표를 위험 기반 목표(Risk-Based Objective) 및 의미 있는 단언과 함께 사용하면 단순한 테스트 실행을 소프트웨어 검증의 깊이(Verification Depth)를 측정할 수 있는 정량적 증거로 전환할 수 있다.

## 01.06. Risk Based Testing Prioritization FMEA Driven

![](images/image6.png){width="7.268055555555556in" height="7.268055555555556in"}

위험 기반 테스트(Risk-Based Testing)는 모든 로봇 소프트웨어에 테스트 자원을 균등하게 배분하는 대신 장애의 결과와 발생 가능성에 따라 검증 활동의 우선순위를 결정한다. 이 접근법은 개발 시간, 하드웨어 접근성, 시뮬레이션(Simulation) 용량 및 현장 테스트(Field Test) 기회가 제한된 상황에서 특히 중요하다. 안전, 임무 실패, 장비 손상 또는 심각한 운용 중단과 관련된 구성요소에는 영향이 작은 기능보다 더 깊고 이른 단계의 테스트를 적용한다.

고장 형태 및 영향 분석(Failure Mode and Effects Analysis, FMEA)은 이러한 우선순위 결정을 위한 체계적인 기반을 제공한다. 엔지니어는 구성요소, 기능, 인터페이스(Interface) 또는 운용 프로세스(Operational Process)를 검토하고 발생 가능한 고장 형태(Failure Mode)를 식별한다. 각각의 고장 형태에 대해 국부적 영향(Local Effect), 연결된 하위 시스템으로의 전파, 시스템 수준 결과, 기존 통제 수단 및 유해한 동작이 발생하기 전에 시스템이나 테스트 프로세스가 문제를 탐지할 수 있는 능력을 분석한다.

로봇 소프트웨어(Robot Software)의 고장 형태는 알고리즘, 통신, 타이밍(Timing), 구성(Configuration), 데이터, 하드웨어 인터페이스 또는 물리적 환경에 대한 잘못된 가정에서 발생할 수 있다. 대표적인 사례에는 오래된 위치추정 데이터(Stale Localization Data), 손상된 센서 측정값, 지연된 제어 명령, 잘못된 좌표 변환(Coordinate Transform), 플래너 교착상태(Planner Deadlock), 액추에이터 포화(Actuator Saturation), 통신 손실, 잘못된 AI 추론(AI Inference), 메모리 고갈 및 비정상 조건 감지 시 안전 상태(Safe State)로 전환하지 못하는 문제가 포함된다.

전통적인 FMEA에서는 일반적으로 심각도(Severity), 발생도(Occurrence), 검출도(Detection)를 평가한다. 심각도는 발생한 결과의 중대성을 나타내고, 발생도는 해당 고장 형태가 발생할 가능성을 추정하며, 검출도는 기존 통제 수단이 허용할 수 없는 결과가 발생하기 전에 문제를 식별할 가능성을 나타낸다. 이러한 요소를 위험 우선순위 수(Risk Priority Number, RPN)로 결합하거나 프로젝트별 위험 매트릭스(Risk Matrix)를 통해 해석할 수 있지만 수치 순위는 엔지니어링 판단(Engineering Judgment)을 대체하는 것이 아니라 지원해야 한다.

물리적 로보틱스(Physical Robotics)에서는 소프트웨어의 의사결정이 실제 운동과 물리적 힘을 발생시킬 수 있으므로 심각도에 특별한 주의가 필요하다. 시각화 오류(Visualization Defect)는 운영자에게 불편을 주는 수준에 머물 수 있지만 잘못된 모션 허가(Motion Permission) 판단은 보호 구역에서 로봇의 움직임을 허용할 수 있다. 마찬가지로 위치추정 오류는 로봇 속도, 환경, 이중화(Redundancy), 오류 감지 및 억제 메커니즘에 따라 단순한 주행 효율 저하에서 충돌 위험까지 다양한 결과를 발생시킬 수 있다.

발생도 추정(Occurrence Estimation)은 가능한 경우 이용할 수 있는 증거를 기반으로 수행해야 한다. 근거에는 결함 이력(Defect History), 현장 텔레메트리(Field Telemetry), 구성요소 복잡도, 인터페이스 불안정성, 시뮬레이션 결과, 이전 세대 로봇의 데이터, 공급업체 정보 또는 엔지니어링 경험 등이 포함될 수 있다. 학습 기반 정책(Learned Policy)이나 새로운 센서와 같은 신기술에서는 발생도 추정에 상당한 불확실성이 존재할 수 있다. 이러한 불확실성 자체가 낮은 위험의 증거가 아니라 추가 테스트가 필요한 이유가 될 수 있다.

검출도 분석(Detection Analysis)은 고장이 시스템 동작에 영향을 미칠 때까지 숨겨진 상태로 남을 가능성이 있는지를 평가한다. 진단 모니터(Diagnostic Monitor), 타당성 검사(Plausibility Check), 감시 타이머(Watchdog), 중복 센서(Redundant Sensor), 명령 검증(Command Validation), 상태 보고(Health Reporting), 런타임 안전 메커니즘(Runtime Safety Mechanism)은 검출 가능성을 향상시킬 수 있다. 발생 가능성이 중간 수준인 고장이라도 운동 또는 임무 수준 동작으로 전파되기 전에 탐지하기 어렵다면 높은 테스트 우선순위를 가질 수 있으므로 이러한 메커니즘 자체를 직접 검증해야 한다.

FMEA 결과는 테스트 우선순위 전략(Test-Prioritization Strategy)으로 변환할 수 있다. 고위험 고장 형태에는 더욱 강력한 요구사항 추적성(Requirements Traceability), 상세한 단위 및 통합 테스트(Unit and Integration Testing), 장애 주입 시나리오(Fault-Injection Scenario), 경계값 테스트(Boundary Testing), 시뮬레이션 캠페인(Simulation Campaign), HIL 검증 및 신중하게 통제된 물리적 테스트를 적용해야 한다. 저위험 기능에는 상대적으로 가벼운 구조적 테스트와 일반적인 회귀 테스트(Regression Testing)를 적용하여 제한된 엔지니어링 자원을 잠재적 결과가 가장 큰 장애에 집중할 수 있다.

위험 기반 우선순위화(Risk-Based Prioritization)는 테스트 실행 순서에도 영향을 준다. 중요 안전 및 제어 로직을 대상으로 하는 빠른 테스트는 모든 소프트웨어 변경마다 실행할 수 있으며, 많은 연산 자원을 요구하는 시뮬레이션 시나리오는 주기적으로 또는 릴리스 후보(Release Candidate) 생성 전에 수행할 수 있다. 이후 HIL 및 실제 로봇 테스트는 저비용 환경만으로 충분히 검증할 수 없는 위험 영역에 집중할 수 있다. 이를 통해 위험 수준과 필요한 증거에 따라 테스트 현실성(Test Realism)을 단계적으로 높일 수 있다.

장애 주입(Fault Injection)은 정상 운용에서는 중요한 고장 형태가 거의 발생하지 않을 수 있기 때문에 FMEA 기반 테스트에서 특히 유용하다. 엔지니어는 센서 데이터 손실, 메시지 지연, 손상된 값, 네트워크 단절, 액추에이터 장애, 잘못된 타임스탬프(Timestamp), 자원 고갈 또는 위치추정 성능 저하를 의도적으로 발생시킬 수 있다. 목적은 단순히 장애를 발생시키는 것이 아니라 탐지, 억제(Containment), 대체 동작(Fallback Behavior), 진단 및 복구 메커니즘이 정의된 요구사항에 따라 동작하는지를 검증하는 것이다.

로봇 시스템은 독립적으로 개발된 많은 구성요소를 결합하므로 인터페이스 장애(Interface Failure)에 특별한 주의가 필요하다. 인지 모듈(Perception Module)이 자체적으로 유효한 출력을 생성하더라도 잘못된 좌표 프레임(Coordinate Frame), 단위(Unit), 타임스탬프 또는 의미 규칙(Semantic Convention)으로 해석되면 위험한 결과가 발생할 수 있다. 따라서 FMEA에서는 구성요소 내부 장애뿐만 아니라 센서, ROS 2 노드(Node), 제어기(Controller), AI 모델, 데이터베이스(Database), 클라우드 서비스(Cloud Service), 외부 플릿 또는 임무 관리 시스템 사이의 가정 불일치도 고려해야 한다.

실시간 로봇 소프트웨어(Real-Time Robot Software)에서는 타이밍 관련 고장 형태도 중요하다. 데이터가 논리적으로 정확하더라도 안전한 제어에 사용하기에는 너무 오래되었을 수 있으며, 물리적 상황이 변경된 이후 명령이 도착할 수도 있다. 따라서 위험 기반 테스트에서는 지연시간(Latency), 지터(Jitter), 데드라인 누락(Missed Deadline), 큐 누적(Queue Buildup), 오래된 데이터 거부(Stale-Data Rejection), 동기화 손실(Synchronization Loss), 타이밍 교란 이후의 복구를 평가해야 한다. 이러한 특성은 격리된 단위 테스트보다 통합, 시뮬레이션 또는 HIL 환경에서 검증해야 하는 경우가 많다.

AI 기반 로봇(AI-Enabled Robot)에서는 FMEA를 기존의 결정론적 소프트웨어 장애보다 넓은 범위로 확장해야 한다. 고장 형태에는 오분류(Misclassification), 신뢰도 보정 오류(Confidence Miscalibration), 분포 외 입력(Out-of-Distribution Input), 인지 사각지대(Perception Blind Spot), 정책 불안정성(Policy Instability), 부적절한 일반화(Inappropriate Generalization), 자원 경합(Resource Contention) 상황에서의 모델 지연시간 등이 포함될 수 있다. 이러한 장애는 데이터 의존적인 경우가 많으므로 기존 소프트웨어 검증과 데이터셋 평가(Dataset Evaluation), 시나리오 커버리지(Scenario Coverage), 강건성 테스트(Robustness Testing), 시뮬레이션 및 통제된 실제 환경 시험을 결합해야 한다.

위험 분석(Risk Analysis)은 별도의 독립적인 테스트 프로세스를 만드는 것이 아니라 테스트 피라미드(Testing Pyramid)와 연결되어야 한다. 하나의 고위험 위험요소(Hazard)는 의사결정 로직을 위한 단위 테스트, 인터페이스를 위한 통합 테스트, 전체 대응을 위한 시스템 테스트(System Test), 환경 변화에 대한 시뮬레이션 시나리오, 타이밍과 하드웨어 동작을 위한 HIL 테스트, 운용 유효성 확인(Operational Validation)을 위한 현장 테스트로 이어질 수 있다. 이를 통해 점진적으로 현실성이 높아지는 검증 환경에서 위험을 반복적으로 평가할 수 있다.

FMEA는 회귀 테스트에도 영향을 주어야 한다. 결함이나 현장 사고(Field Incident)를 통해 이전에 과소평가된 고장 형태가 발견되면 해당 위험 평가를 다시 검토하고 가능한 가장 낮은 테스트 수준에 적절한 회귀 테스트를 추가해야 한다. 심각한 장애는 여러 테스트 수준에 대응하는 시나리오를 추가해야 할 수도 있다. 이러한 방식으로 운용 경험(Operational Experience)은 사고 보고서에만 남지 않고 위험 모델과 자동화 검증 스위트(Automated Verification Suite)를 지속적으로 개선한다.

추적성(Traceability)을 사용하면 고장 형태를 위험요소, 요구사항, 완화 조치(Mitigation), 테스트 케이스(Test Case), 결과 및 잔여 위험(Residual Risk)과 연결할 수 있다. 고위험 FMEA 항목은 완화 조치가 구현되었다는 이유만으로 관리 대상에서 사라져서는 안 되며, 관련 조건에서 해당 완화 조치가 실제로 동작한다는 증거가 필요하다. 위험 기록(Risk Record)을 검증 산출물(Verification Artifact)과 연결하면 기술 검토, 릴리스 결정, 안전 사례(Safety Case), 이후 공식 적합성 활동에서 요구되는 인증 증거(Certification Evidence)도 지원할 수 있다.

위험 기반 테스트를 하나의 위험 우선순위 수(Risk Priority Number)만으로 테스트를 정렬하는 방식으로 축소해서는 안 된다. 심각도, 발생도, 검출도의 서로 다른 조합이 유사한 수치 값을 생성하더라도 필요한 엔지니어링 대응은 서로 다를 수 있다. 발생 빈도가 낮더라도 극도로 심각한 위험은 종합 점수가 중간 수준이더라도 엄격한 테스트가 필요할 수 있으며, 불확실성이 큰 고장 형태에는 탐색적 테스트(Exploratory Testing)가 필요할 수 있다. 따라서 전문가 검토(Expert Review)와 명확한 판단 근거가 우선순위 결정의 필수 요소로 유지되어야 한다.

위험 모델(Risk Model)은 로봇 아키텍처, 소프트웨어, 하드웨어, 운용 환경 및 현장 증거가 변화함에 따라 지속적으로 발전해야 한다. 새로운 센서, AI 모델, 제어 전략, 페이로드(Payload), 펌웨어(Firmware), 배포 환경은 초기 분석에는 존재하지 않았던 새로운 고장 형태를 도입할 수 있다. 따라서 정기적인 FMEA 검토, 변경 영향 분석(Change-Impact Analysis), 결함 추세, 텔레메트리 및 사고 데이터를 테스트 선택, 커버리지 목표(Coverage Objective), 릴리스 기준(Release Criteria)에 지속적으로 반영해야 한다.

성숙한 FMEA 기반 테스트 전략(FMEA-Driven Testing Strategy)은 궁극적으로 위험 분석을 측정 가능한 검증 활동으로 변환한다. 조직은 단순히 테스트가 몇 개 존재하는지 또는 코드의 몇 퍼센트가 커버되는지를 묻는 데 그치지 않고, 가장 중대한 결과를 초래할 수 있는 장애가 식별되고 시험되었으며 탐지·억제되고 검증되었는지를 확인한다. 이를 통해 엔지니어링 위험(Engineering Risk), 테스트 깊이(Testing Depth), 자원 배분(Resource Allocation), 그리고 정상 및 비정상 조건에서 로봇이 신뢰성 있게 운용될 수 있음을 보여주는 증거 사이에 직접적인 관계를 구축할 수 있다.

## 01.07. Test Environment Management Isolation Reproducibility

![](images/image7.png){width="7.268055555555556in" height="7.268055555555556in"}

테스트 환경 관리(Test Environment Management)는 로봇 소프트웨어(Robot Software)를 검증 및 유효성 확인(Verification and Validation)하는 통제된 조건을 확립한다. 엔지니어가 테스트 결과를 생성한 소프트웨어 버전, 의존성(Dependency), 구성(Configuration), 하드웨어 상태, 테스트 데이터, 시뮬레이터 설정 및 환경적 가정을 식별할 수 있어야 테스트 결과가 의미를 가진다. 체계적인 환경 관리가 없으면 장애를 재현하기 어려워지고 성공한 테스트 결과도 이후 릴리스(Release)에 대한 신뢰성 있는 증거를 제공하지 못할 수 있다.

격리(Isolation)는 신뢰할 수 있는 테스트 환경의 기본적인 특성이다. 각각의 테스트는 이전 테스트, 병렬 프로세스(Parallel Process), 개발자 장비, 공유 서비스(Shared Service), 영구 파일, 네트워크 상태 또는 물리적 하드웨어 이력으로부터 발생하는 의도하지 않은 영향을 최소화해야 한다. 다른 테스트가 매개변수를 초기화하거나 데이터베이스를 채우고, 캐시(Cache)를 준비하거나 ROS 2 노드를 실행 상태로 남겨두었기 때문에 통과하는 테스트는 숨겨진 의존성을 형성하여 잘못된 결과를 생성할 수 있다.

따라서 소프트웨어 의존성(Software Dependency)은 명시적으로 통제해야 한다. 컴파일러(Compiler) 버전, 운영체제 패키지, Python 라이브러리, ROS 2 배포판(Distribution), 미들웨어(Middleware) 구현, GPU 런타임(Runtime), 장치 드라이버(Device Driver), 시뮬레이션 엔진(Simulation Engine), AI 프레임워크(AI Framework)는 모두 로봇의 동작에 영향을 줄 수 있다. 오늘 실행한 테스트를 이후에도 호환되지 않는 라이브러리나 런타임 변경사항을 의도하지 않게 포함하지 않고 재구성할 수 있도록 의존성 버전을 고정하거나 기록해야 한다.

컨테이너화(Containerization)는 소프트웨어 의존성을 격리하기 위한 실용적인 방법 중 하나이다. 컨테이너(Container)는 애플리케이션 바이너리(Application Binary), 라이브러리, 런타임 설정 및 테스트 도구를 반복 가능한 실행 환경으로 패키징하여 개발자 워크스테이션(Workstation)과 지속적 통합(Continuous Integration, CI) 인프라에서 일관되게 동작하도록 할 수 있다. 그러나 커널(Kernel) 동작, GPU 드라이버, 물리 장치, 네트워크 구성, 타이밍 및 외부 서비스는 호스트마다 달라질 수 있으므로 컨테이너만으로 재현성이 자동으로 보장되는 것은 아니다.

구성 관리(Configuration Management)도 중요하다. 로봇의 동작은 소스 코드(Source Code)뿐만 아니라 매개변수(Parameter)에 의해 결정되는 경우가 많기 때문이다. 제어기 게인(Controller Gain), 센서 캘리브레이션(Sensor Calibration), 좌표 프레임(Coordinate Frame), 플래너 제한값(Planner Limit), 안전 임계값(Safety Threshold), 모델 경로(Model Path), QoS 설정, 지도 버전 및 실행 매개변수(Launch Parameter)는 버전 관리되거나 고유하게 식별할 수 있어야 한다. 소프트웨어 커밋(Commit)만 기록하고 사용된 구성을 기록하지 않은 테스트 보고서로는 테스트 당시의 로봇 상태를 완전하게 재구성할 수 없다.

테스트 데이터(Test Data) 역시 환경의 일부로 관리해야 한다. 센서 기록, 지도, 캘리브레이션 파일, 합성 데이터셋(Synthetic Dataset), 기준 궤적(Reference Trajectory), 예상 출력, AI 모델 및 시나리오 정의(Scenario Definition)는 안정적인 식별자와 통제된 버전을 가져야 한다. 로스백(rosbag), 포인트 클라우드(Point Cloud), 이미지 데이터셋 또는 지도가 동일한 이름을 유지한 상태에서 변경되면 동일한 테스트 코드가 명확한 원인 없이 다른 결과를 생성하여 재현성과 회귀 분석(Regression Analysis)의 신뢰성을 저하시킬 수 있다.

가능한 경우 결정론적 실행(Deterministic Execution)을 추구해야 한다. 난수 생성기(Random-Number Generator)는 기록된 시드(Seed)를 사용하고, 시나리오 초기화는 정의된 절차를 따라야 하며, 시뮬레이션 시간(Simulation Time)은 통제되어야 한다. 또한 비동기 프로세스(Asynchronous Process)는 불필요하게 실제 시계 시간(Wall-Clock Timing)에 의존하지 않도록 해야 한다. 분산 로보틱스, GPU 연산, 물리 시뮬레이션 또는 학습 시스템에서는 완전한 결정성을 달성하기 어려울 수 있으므로 통계적으로 정의된 허용오차와 반복 시험을 통해 재현성을 확보할 수도 있다.

ROS 2 환경에서는 디스커버리(Discovery), 네임스페이스(Namespace), 도메인 식별자(Domain Identifier), QoS 정책, 변환(Transform), 수명주기 상태(Lifecycle State)로 인해 서로 독립적이어야 하는 테스트가 간섭할 수 있으므로 격리에 특별한 주의가 필요하다. 별도의 ROS 도메인 또는 네트워크 네임스페이스(Network Namespace)를 사용하여 테스트 인스턴스를 격리하고, 고유한 노드 이름과 임시 자원을 사용하여 충돌을 줄일 수 있다. 테스트 종료(Teardown) 과정에서는 노드를 확실하게 종료하고 임시 상태를 제거하여 다음 실행이 알려진 기준 상태에서 시작되도록 해야 한다.

외부 서비스(External Service)는 또 다른 비결정성(Nondeterminism)의 원인이 된다. 로봇 소프트웨어는 데이터베이스, 플릿 서버(Fleet Server), 클라우드 API(Cloud API), 지도 서비스, 인증 시스템(Authentication System), 텔레메트리 백엔드(Telemetry Backend)에 의존할 수 있으며 이러한 서비스의 가용성과 데이터는 시간에 따라 변경된다. 단위 및 통합 환경에서는 필요한 경우 외부 서비스를 통제된 대체 서비스로 교체하고, 전용 시스템 환경에서는 버전이 관리되는 서비스 인스턴스를 배포할 수 있다. 선택하는 방법은 해당 테스트가 무엇을 검증하려는지에 따라 결정해야 한다.

시뮬레이션 환경(Simulation Environment)은 일반적인 소프트웨어 의존성보다 더 광범위한 구성 통제가 필요하다. 물리 엔진(Physics Engine) 버전, 시간 간격(Time Step), 솔버(Solver) 설정, 센서 노이즈 모델(Sensor Noise Model), 환경 자산(Environment Asset), 로봇 모델, 충돌 특성(Collision Property), 마찰 계수(Friction Coefficient), 조명, 무작위화 매개변수(Randomization Parameter), 시나리오 시드는 결과에 실질적인 영향을 미칠 수 있다. 따라서 시뮬레이션 장애를 재현하려면 애플리케이션 소프트웨어뿐만 아니라 시뮬레이션 월드(Simulation World)와 실행 매개변수도 함께 보존해야 한다.

하드웨어 인 더 루프(Hardware-in-the-Loop, HIL) 환경은 실제 제어기와 인터페이스가 테스트에 참여하기 때문에 추가적인 구성 요소를 관리해야 한다. 펌웨어(Firmware) 버전, 배선(Wiring), 입출력 매핑(I/O Mapping), 버스 구성(Bus Configuration), 캘리브레이션, 전원 조건, 실시간 시뮬레이터 모델(Real-Time Simulator Model), 테스트 장비를 기록해야 한다. 자동화된 환경 검사를 통해 실행 전에 HIL 벤치(Bench)가 예상 상태에 있는지 확인하면 잘못 구성된 실험실 환경 때문에 유효하지 않은 결과가 발생하는 것을 방지할 수 있다.

실제 로봇 테스트 환경(Physical Robot Test Environment)에서는 더욱 엄격한 상태 관리가 필요하다. 배터리 상태, 페이로드(Payload), 타이어 상태, 관절 캘리브레이션(Joint Calibration), 센서 청결 상태, 온도, 네트워크 연결, 지도 버전, 안전 구성 및 기계적 변경사항은 모두 테스트 결과에 영향을 줄 수 있다. 반복 가능한 테스트 프로토콜(Test Protocol)은 준비 및 초기화 절차를 명확하게 정의하여 실행 간 차이가 로봇이나 시설의 통제되지 않은 변화가 아니라 실제 조사 대상 변수에서 발생하도록 해야 한다.

가능한 경우 테스트 환경 프로비저닝(Environment Provisioning)을 자동화해야 한다. 인프라 스크립트(Infrastructure Script), 컨테이너 정의(Container Definition), 패키지 잠금 파일(Package Lock File), 실행 구성, 시뮬레이션 매니페스트(Simulation Manifest), 설정 절차를 사용하면 수동 작업으로 인한 편차를 줄이면서 알려진 테스트 환경을 재구성할 수 있다. 지속적 통합은 환경을 생성하고 테스트를 실행하며 증거를 보관한 후 임시 자원을 제거할 수 있다. 불변 환경(Immutable Environment) 또는 단기 환경(Short-Lived Environment)은 구성 드리프트(Configuration Drift)를 줄이고 장애를 원래 실행 시스템 외부에서도 쉽게 재현할 수 있도록 한다.

환경 검증(Environment Validation)은 프로비저닝이 성공했다고 가정하지 말고 테스트 실행 전에 수행해야 한다. 자동화된 사전 점검(Preflight Check)을 통해 소프트웨어 버전, 사용 가능한 장치, 네트워크 연결, 시간 동기화(Time Synchronization), 저장 공간, GPU 접근 가능성, 캘리브레이션 식별자, 안전 상태 및 필요한 서비스를 확인할 수 있다. 필수 조건이 올바르지 않다면 제품의 실패 또는 성공으로 잘못 보고하지 말고 테스트 환경 실패(Environment Failure)로 분류해야 한다.

재현성(Reproducibility)을 확보하려면 포괄적인 테스트 메타데이터(Test Metadata)도 필요하다. 결과에는 소스 리비전(Source Revision), 빌드 산출물(Build Artifact), 구성 해시(Configuration Hash), 의존성 버전, 테스트 데이터 버전, 환경 이미지(Environment Image), 하드웨어 식별자, 타임스탬프(Timestamp), 난수 시드, 시나리오 매개변수 및 관련 로그(Log)를 포함해야 한다. 이러한 메타데이터는 장애가 발생한 조건을 엔지니어가 재구성하고 소프트웨어 회귀와 환경 변화의 영향을 구분할 수 있도록 출처 추적 체계(Provenance Chain)를 형성한다.

불안정 테스트(Flaky Test)는 불충분한 격리 또는 통제되지 않은 비결정성을 나타내는 중요한 경고 신호이다. 실패한 테스트가 통과할 때까지 반복 실행하는 방식은 경쟁 상태(Race Condition), 타이밍 가정, 자원 경합(Resource Contention), 공유 상태 누출(Shared-State Leakage), 불안정한 인프라를 숨길 수 있다. 불안정성(Flakiness)은 엔지니어링 결함으로 측정하고 조사해야 한다. 테스트 격리(Quarantine)를 통해 일시적으로 파이프라인을 보호할 수는 있지만 비결정성의 근본 원인은 계속 식별하고 수정해야 한다.

환경 관리는 테스트 수준마다 서로 다른 형태의 통제가 필요하므로 전체 테스트 계층(Test Hierarchy)에 걸쳐 적용되어야 한다. 소프트웨어 테스트는 의존성과 프로세스 격리를 강조하고, 시뮬레이션은 모델과 시나리오 통제를 추가하며, HIL은 물리적 인터페이스와 실시간 장비를 추가하고, 현장 테스트(Field Testing)는 환경 및 운용 변수를 추가한다. 따라서 테스트가 실제 시스템에 가까워질수록 통제해야 하는 환경 변수의 범위와 복잡성도 함께 증가한다.

효과적인 재현성 전략(Reproducibility Strategy)은 정확한 반복(Exact Repetition)과 대표성 있는 반복(Representative Repetition)을 구분한다. 단위 테스트는 일반적으로 거의 동일한 결과를 반복적으로 생성해야 하지만 확률적 AI 평가(Stochastic AI Evaluation)나 실제 현장 시험은 자연스럽게 변동할 수 있다. 후자의 경우 재현성은 개별 측정값을 완전히 동일하게 만드는 것이 아니라 실험 프로토콜, 분포(Distribution), 합격 기준(Acceptance Criteria), 표본 크기(Sample Size), 분석 방법을 보존하여 반복된 시험 캠페인이 통계적으로 비교 가능한 결론을 생성하도록 하는 것을 의미한다.

테스트 환경은 공식적인 변경 통제(Change Control) 아래에서 발전해야 한다. 운영체제, 시뮬레이터, 컴파일러, 펌웨어, 드라이버, AI 런타임 또는 캘리브레이션을 변경하면 애플리케이션 소스 코드가 동일하더라도 과거 결과와의 비교가 무효화될 수 있다. 따라서 환경 변경에는 영향 분석(Impact Analysis)을 수행하고 필요한 경우 기준선 재생성(Baseline Regeneration) 또는 회귀 테스트를 실행해야 한다. 환경 자체를 버전이 관리되는 엔지니어링 산출물(Versioned Engineering Artifact)로 취급하면 인프라 변경이 보이지 않는 실험 변수로 작용하는 것을 방지할 수 있다.

성숙한 로보틱스 조직(Robotics Organization)은 궁극적으로 격리와 재현성을 개발자의 편의를 위한 기능이 아니라 검증 시스템(Verification System)의 핵심 속성으로 취급한다. 중요한 모든 테스트는 로봇 소프트웨어가 통과했는지만 확인하는 것이 아니라 정확히 무엇을, 어떤 조건에서 테스트했으며 해당 조건을 다시 재현할 수 있는지까지 설명할 수 있어야 한다. 이러한 원칙을 적용하면 테스트 결과를 디버깅(Debugging), 회귀 분석, 릴리스 결정, 유효성 확인, 인증(Certification)을 지원할 수 있는 지속 가능한 엔지니어링 증거(Durable Engineering Evidence)로 전환할 수 있다.

## 01.08. Test Data Management for Robot SW

![](images/image8.png){width="7.268055555555556in" height="7.268055555555556in"}

테스트 데이터 관리(Test Data Management)는 로봇 소프트웨어(Robot Software)를 검증하는 데 사용되는 데이터셋(Dataset), 기록 데이터, 구성(Configuration), 기준 출력(Reference Output), 시나리오 입력(Scenario Input)을 생성하고 식별하며 저장·버전 관리·배포·폐기하는 방법을 정의한다. 로봇의 동작은 센서 관측값과 환경 조건에 크게 의존하므로 실행 과정에서 사용된 정확한 데이터를 식별하고 재현할 수 없다면 테스트 결과를 신뢰성 있게 해석하기 어렵다.

로봇 테스트 데이터(Robot Test Data)는 다양한 출처에서 생성될 수 있다. 단위 테스트(Unit Test)는 작은 합성 입력(Synthetic Input)과 사전에 정의된 예상값을 사용할 수 있으며, 통합 테스트(Integration Test)는 기록된 ROS 2 메시지, 지도, 궤적 또는 데이터베이스 픽스처(Database Fixture)를 사용할 수 있다. 시뮬레이션(Simulation)은 시나리오 구성과 합성 센서 스트림(Synthetic Sensor Stream)을 생성하며, 현장 테스트(Field Testing)는 카메라, 라이다(LiDAR), 레이더(Radar), IMU, GNSS, 액추에이터, 진단, 네트워크 및 임무 텔레메트리(Mission Telemetry)를 대량으로 생성하므로 체계적인 관리가 필요하다.

유용한 테스트 데이터셋(Test Dataset)은 단순히 사용 가능한 데이터를 축적하는 것이 아니라 명확한 목적을 가져야 한다. 각각의 데이터셋은 정상 운용(Nominal Operation), 경계 조건(Boundary Condition), 알려진 결함(Known Defect), 안전 관련 상황, 환경 변화, 하드웨어 장애 또는 과거에 관찰된 현장 사고(Field Incident)를 나타낼 수 있다. 데이터셋을 요구사항, 위험(Risk), 테스트 케이스(Test Case), 예상 동작과 연결하면 단순한 로봇 활동 기록이 아니라 재사용 가능한 검증 자산(Verification Asset)으로 활용할 수 있다.

테스트 데이터가 변경되면 소프트웨어가 동일하더라도 테스트 결과가 달라질 수 있으므로 버전 관리(Version Control)가 필수적이다. 로스백(rosbag), 이미지, 포인트 클라우드(Point Cloud), 지도, 신경망 모델(Neural-Network Model), 시뮬레이션 기록과 같은 대용량 바이너리 산출물(Binary Artifact)은 일반적인 소스 저장소와 별도의 저장 시스템이 필요할 수 있다. 저장 기술과 관계없이 각각의 데이터셋에는 테스트 결과가 정확한 입력을 식별할 수 있도록 안정적인 식별자, 버전, 체크섬(Checksum) 또는 불변 참조(Immutable Reference)가 존재해야 한다.

메타데이터(Metadata)는 기록된 데이터를 올바르게 해석하는 데 필요한 맥락을 제공한다. 로보틱스 데이터셋(Robotics Dataset)에는 타임스탬프(Timestamp), 센서 모델, 캘리브레이션 식별자(Calibration Identifier), 좌표 프레임(Coordinate Frame), 샘플링 주파수, 단위(Unit), 펌웨어(Firmware) 버전, 로봇 구성, 페이로드(Payload), 지도 버전, 날씨, 조명, 위치 유형, 운용 모드 및 소프트웨어 리비전(Software Revision)이 필요할 수 있다. 이러한 정보가 없으면 가치 있어 보이는 센서 기록도 수집 당시의 조건을 재구성하기 어려워 재사용 가치가 감소할 수 있다.

다중 센서 로봇 데이터(Multi-Sensor Robot Data)에서는 시간 동기화(Time Synchronization)가 특히 중요하다. 센서 융합(Sensor Fusion)이나 인과관계 동작(Causal Behavior)을 평가할 때 카메라 프레임, LiDAR 스캔, IMU 측정값, GNSS 관측값, 관절 상태(Joint State), 제어 명령 및 진단 이벤트를 일관된 시간 기준에 연결해야 한다. 따라서 데이터셋 메타데이터에는 해석에 영향을 미치는 경우 클록 소스(Clock Source), 동기화 상태, 타임스탬프 의미 체계(Timestamp Semantics), 알려진 시간 오차를 보존해야 한다.

캘리브레이션 정보(Calibration Information)도 테스트 데이터와 연계하여 유지해야 한다. 카메라 내부 파라미터(Camera Intrinsics), 센서 외부 파라미터(Sensor Extrinsics), LiDAR 정렬, IMU 캘리브레이션, 휠 파라미터(Wheel Parameter), 관절 오프셋(Joint Offset), 좌표 변환(Coordinate Transform)은 로봇의 수명주기 동안 변경될 수 있다. 과거 데이터를 더 새로운 캘리브레이션 파일로 재생하면 원래 실험과 다른 결과가 발생할 수 있으므로 테스트에서는 최신 값을 무조건 사용하는 대신 해당 데이터셋에 대응하는 캘리브레이션 버전을 참조해야 한다.

골든 데이터(Golden Data) 또는 기준선(Baseline)이라고도 하는 기준 출력(Reference Output)은 예상 동작이 충분히 안정적인 경우 회귀 테스트(Regression Testing)를 지원할 수 있다. 위치추정 알고리즘(Localization Algorithm)은 기준 자세(Reference Pose)와 비교하고, 파서(Parser)는 알려진 디코딩 메시지와 비교하며, 궤적 생성기(Trajectory Generator)는 승인된 출력 특성과 비교할 수 있다. 그러나 과거 출력을 자동으로 정답으로 간주하면 기존 결함을 그대로 유지하거나 정당한 알고리즘 개선을 방해할 수 있으므로 기준선은 신중하게 검토해야 한다.

테스트 데이터에는 성공적인 정상 운용뿐만 아니라 비정상 조건(Abnormal Condition)과 경계 조건도 포함해야 한다. 센서 데이터 손실, 잘못된 타임스탬프, 손상된 메시지, 극단적인 측정 범위, 통신 손실, 위치추정 성능 저하, 액추에이터 포화(Actuator Saturation), 비정상적인 객체 배치 및 복구 이벤트(Recovery Event)는 일반적인 기록에서 거의 실행되지 않는 로직을 노출할 수 있다. FMEA 기반 위험 분석(FMEA-Driven Risk Analysis)을 활용하면 회귀 테스트 스위트에서 어떤 장애 중심 데이터셋에 높은 우선순위를 부여해야 하는지 결정할 수 있다.

현장 사고(Field Incident)는 특히 가치 있는 회귀 데이터(Regression Data)의 원천이다. 배포된 로봇이 예상하지 못한 장애물 배치, 위치추정 실패, 통신 장애, 플래너 오류(Planner Error) 또는 비정상적인 인간 상호작용을 경험하면 관련 로그를 추출하여 재현 가능한 테스트 자산으로 변환할 수 있다. 근본적인 결함을 수정한 이후에도 사고 데이터셋을 회귀 테스트 스위트에 유지하면 향후 소프트웨어 버전이 동일한 조건에 다시 노출되도록 할 수 있다.

원시 로봇 기록(Raw Robot Recording)은 매우 커질 수 있으므로 데이터 축소(Data Reduction)가 필요한 경우가 많다. 연속적인 고해상도 카메라와 LiDAR 스트림은 장기간 보존하기 어려울 정도로 많은 데이터를 생성할 수 있다. 중요한 사건에 대해서는 전체 증거를 보존하면서 관련 장애, 대표 시나리오 또는 경계 조건 주변의 작은 구간을 추출할 수 있다. 데이터 축소 절차는 재현에 필요한 정보를 유지해야 하며 테스트의 의미를 변경하는 맥락을 제거하지 않아야 한다.

데이터셋 품질(Dataset Quality)은 소프트웨어와 마찬가지로 검증이 필요하다. 자동화 검사를 통해 누락된 파일, 손상된 기록, 일관되지 않은 타임스탬프, 잘못된 스키마(Schema), 불가능한 값, 불완전한 캘리브레이션, 중복 샘플 또는 손상된 참조를 식별할 수 있다. 데이터셋이 알 수 없는 상태에서 변경되거나 잘못된 입력을 포함하면 거짓 회귀(False Regression)나 잘못된 테스트 통과를 발생시킬 수 있다. 무결성 검사(Integrity Check)와 체크섬을 사용하면 실제 소프트웨어 동작 변화와 손상된 테스트 자산을 구분하는 데 도움이 된다.

로봇 데이터셋에 사람, 시설, 차량 식별자, 오디오, 운용 배치 정보 또는 고객 정보가 포함되는 경우 접근 통제(Access Control)와 개인정보 보호(Privacy)가 중요해질 수 있다. 테스트 데이터 파이프라인(Test-Data Pipeline)은 민감한 기록에 접근할 수 있는 주체, 보존 기간, 익명화(Anonymization) 필요 여부 및 복사 가능한 위치를 정의해야 한다. 개발 편의성을 이유로 실제 운용에서 생성된 데이터를 적절한 거버넌스(Governance)와 보안 통제 없이 배포해서는 안 된다.

실제 환경 사례가 부족하거나 위험하고 비용이 높으며 재현하기 어려운 경우 시뮬레이션 및 합성 데이터(Synthetic Data)를 대안으로 활용할 수 있다. 통제된 데이터 생성을 통해 조명, 지형, 장애물 배치, 센서 노이즈(Sensor Noise), 날씨, 페이로드 또는 장애 조건을 체계적으로 변화시킬 수 있다. 합성 데이터셋 역시 시나리오를 재구성하고 소프트웨어 리비전 간 결과를 비교할 수 있도록 생성기 버전(Generator Version), 월드 자산(World Asset), 난수 시드(Random Seed), 매개변수 분포(Parameter Distribution), 시뮬레이터 구성을 보존해야 한다.

AI 기반 로봇 테스트(AI-Enabled Robot Testing)는 모델 동작이 개별 사례뿐만 아니라 데이터 분포(Data Distribution)에 의존하기 때문에 더욱 광범위한 데이터 관리가 필요하다. 필요한 경우 평가 데이터셋(Evaluation Set)을 학습(Training), 검증(Validation), 회귀, 안전, 엣지 케이스(Edge Case), 분포 외(Out-of-Distribution, OOD) 데이터로 구분해야 한다. 데이터셋 누출(Dataset Leakage)을 방지해야 하며 샘플 구성이 변경되면 모델 자체가 변경되지 않았더라도 보고되는 정확도, 강건성(Robustness), 작업 성공률(Task-Success Metric)이 달라질 수 있으므로 평가 데이터셋의 변경도 버전 관리해야 한다.

데이터셋의 크기만큼 대표성(Representativeness)도 중요하다. 거의 동일한 수백만 개의 관측값보다 객체, 환경, 속도, 페이로드, 조명, 지형, 인간 행동 및 장애 조건에서 의미 있는 변화를 포함하는 더 작은 데이터 집합이 높은 검증 가치를 제공할 수 있다. 따라서 커버리지 분석(Coverage Analysis)은 파일, 프레임(Frame), 주행거리 또는 기록 시간의 단순한 개수뿐만 아니라 시나리오 및 운용 영역(Operational Domain)의 다양성까지 고려해야 한다.

테스트 데이터는 지속적 테스트(Continuous Testing)와 통합하여 서로 다른 테스트 스위트가 올바른 버전을 자동으로 가져올 수 있도록 해야 한다. 빠른 단위 테스트에서는 소스 코드와 함께 저장된 작은 픽스처(Fixture)를 사용할 수 있고, 대규모 통합 및 시뮬레이션 테스트에서는 관리형 저장소에서 불변 산출물을 가져올 수 있다. 릴리스 유효성 확인(Release Validation)에서는 내용이 고정되고 검토되며 특정 인수 기준(Acceptance Criteria)에 연결된 인증된 데이터셋 집합을 참조함으로써 후보 소프트웨어 버전 사이의 일관된 비교를 가능하게 할 수 있다.

추적성(Traceability)은 테스트 데이터를 전체 검증 프로세스와 연결한다. 테스트 결과는 소프트웨어 빌드(Software Build)와 환경뿐만 아니라 데이터셋 식별자, 구성, 캘리브레이션, 시나리오 정의, 예상 출력 및 분석 버전(Analysis Version)을 식별할 수 있어야 한다. 이러한 원칙은 소프트웨어 통합, 시뮬레이션, 하드웨어 인 더 루프(Hardware-in-the-Loop, HIL), 현장 테스트 및 AI 평가(AI Evaluation) 전반으로 확장되며, 이들 모든 단계는 통제된 증거와 반복 가능한 입력에 의존한다.

보존 및 수명주기 정책(Retention and Lifecycle Policy)은 테스트 저장소가 통제되지 않는 아카이브(Archive)로 변하는 것을 방지한다. 안전 증거(Safety Evidence), 인증, 현장 사고 또는 릴리스 기준선과 관련된 고가치 데이터셋은 장기간 보존해야 할 수 있는 반면 임시 디버그 기록(Debug Recording)은 정의된 기간 이후 삭제할 수 있다. 대체된 데이터셋은 이를 사용했던 과거 테스트 결과에 대한 추적성을 손상시키지 않으면서 통제된 방식으로 보관하거나 폐기해야 한다.

성숙한 로보틱스 조직(Robotics Organization)은 궁극적으로 테스트 데이터를 소스 코드 및 구성과 동일한 수준의 버전 관리 엔지니어링 자산(Versioned Engineering Asset)으로 취급한다. 목표는 단순히 대량의 센서 정보를 저장하는 것이 아니라 검증에 사용할 수 있는 신뢰성 있고 대표적이며 추적 가능하고 재현 가능한 입력을 유지하는 것이다. 효과적인 테스트 데이터 관리는 현장 경험, 시뮬레이션 시나리오, 알려진 장애 및 예상 동작을 재사용 가능한 증거로 전환하여 로봇 소프트웨어 품질을 지속적으로 강화한다.

## 01.09. Continuous Testing Philosophy Shift Left

![](images/image9.png){width="7.268055555555556in" height="7.268055555555556in"}

지속적 테스트(Continuous Testing)는 소프트웨어 수명주기(Software Lifecycle)의 후반부나 릴리스(Release) 직전에 검증 활동을 집중하는 대신 개발 전 과정에서 지속적으로 검증을 수행하는 개발 철학이다. 로봇 소프트웨어(Robot Software)에서는 코드, 인터페이스(Interface), 알고리즘, 구성(Configuration), 모델(Model), 시스템 동작이 변경될 때마다 지속적으로 평가하는 것을 의미한다. 목표는 결함이 생성된 시점과 발견되는 시점 사이의 시간을 단축하여 일반적으로 진단과 수정 비용이 더 낮은 단계에서 문제를 해결하는 것이다.

시프트 레프트 테스트(Shift-Left Testing)는 검증 활동을 개발의 더 이른 단계로 이동시킨다. 통합된 로봇에서 문제가 드러날 때까지 기다리는 대신 요구사항 정의, 아키텍처(Architecture), 상세 설계 및 구현 단계부터 테스트를 시작한다. 요구사항은 테스트 가능성(Testability)을 기준으로 검토하고, 인터페이스는 측정 가능한 계약(Measurable Contract)으로 명세하며, 소프트웨어 구성요소는 비용이 높은 시뮬레이션(Simulation), HIL 또는 실제 로봇 테스트가 필요해지기 전에 독립적으로 검증할 수 있도록 설계한다.

시프트 레프트 철학(Shift-Left Philosophy)은 단순히 단위 테스트(Unit Test)를 더 일찍 실행하는 것을 의미하지 않는다. 테스트에 대한 고려사항이 개발 초기부터 엔지니어링 의사결정에 영향을 미치도록 해야 한다. 예를 들어 "로봇은 안전하게 정지해야 한다"라는 요구사항은 응답시간(Response Time), 정지거리(Stopping Distance), 속도 또는 안전구역 경계(Safety-Zone Boundary)와 관련된 측정 가능한 기준으로 변환해야 한다. 이러한 조건을 조기에 정의하면 모호한 기대사항이 통합 및 현장 테스트(Field Testing) 단계까지 전달되는 것을 방지할 수 있으며, 후반 단계에서 이를 해결하는 데 필요한 비용을 크게 줄일 수 있다.

시프트 레프트 개발(Shift-Left Development)에서는 아키텍처 역시 중요한 테스트 활동의 대상이 된다. 엔지니어는 구현이 완료되기 전에 구성요소 경계, 인터페이스, 타이밍 가정(Timing Assumption), 장애 대응(Failure Response), 의존성(Dependency)을 식별한다. ROS 2 노드(Node), 라이브러리(Library), 하드웨어 추상화 계층(Hardware Abstraction Layer), 상태 머신(State Machine), AI 추론 구성요소(AI Inference Component)는 결정론적 로직(Deterministic Logic)을 하드웨어 및 통신 메커니즘과 분리하도록 구성할 수 있다. 이를 통해 완전한 로봇 없이도 저비용 테스트로 중요한 동작을 검증할 수 있다.

테스트 주도 개발(Test-Driven Development, TDD)과 행동 주도 개발(Behavior-Driven Development, BDD)은 지속적인 시프트 레프트 테스트를 강화한다. TDD는 상세 구현 전에 실행 가능한 기대 동작(Executable Expectation)을 생성하고, BDD는 여러 엔지니어링 분야가 이해할 수 있는 시나리오(Scenario)를 통해 운용 동작을 표현한다. 두 방법을 함께 사용하면 소프트웨어 복잡도가 증가하기 전에 올바른 동작의 의미를 명확하게 정의할 수 있다. 따라서 테스트는 구현이 안정화된 이후에 생성하는 산출물이 아니라 실행 가능한 엔지니어링 명세(Executable Engineering Specification)가 된다.

정적 분석(Static Analysis)은 소프트웨어를 실행하지 않고도 많은 결함을 발견할 수 있기 때문에 또 다른 초기 검증 계층을 제공한다. 컴파일러 경고(Compiler Warning), 타입 검사(Type Checking), 코딩 규칙 분석(Coding-Rule Analysis), 의존성 검사(Dependency Scanning), 포맷 검사(Formatting Check), 복잡도 분석(Complexity Analysis), 보안 검사(Security Inspection)를 통해 코드 변경 직후 문제를 식별할 수 있다. 이러한 검사는 실제 로봇 테스트보다 비용이 낮고 빈번하게 실행할 수 있으므로 개발자 워크스테이션(Workstation), 사전 커밋(Pre-Commit) 워크플로 및 지속적 통합(Continuous Integration, CI) 파이프라인에 적합하다.

빠른 자동화 단위 테스트(Automated Unit Test)는 지속적 테스트의 기반을 형성한다. 수학 유틸리티, 좌표 변환(Coordinate Transformation), 필터(Filter), 파서(Parser), 상태 머신, 명령 검증기(Command Validator), 제어기 계산(Controller Calculation), 계획 함수(Planning Function)는 코드가 변경될 때마다 평가할 수 있다. 모의 객체(Mock), 스텁(Stub), 의존성 주입(Dependency Injection), 기록된 입력을 사용하면 테스트 로직을 카메라, LiDAR, 모터 제어기(Motor Controller), 네트워크 또는 테스트 실행 빈도를 제한할 수 있는 기타 하드웨어로부터 격리할 수 있다.

완전한 시스템이 존재하기 전에 인터페이스를 검증할 수 있다면 통합 테스트(Integration Testing) 역시 가능한 한 시프트 레프트 방식으로 수행해야 한다. ROS 2 메시지 계약(Message Contract), 토픽(Topic), 서비스(Service), 액션(Action), QoS 정책, 변환(Transform), 수명주기 전이(Lifecycle Transition), 타임스탬프(Timestamp), 노드 시작 동작을 통제된 환경에서 테스트할 수 있다. 많은 로보틱스 결함은 개별 알고리즘 자체보다 단위, 프레임(Frame), 타이밍, 구성 및 데이터 의미 체계(Data Semantics)에 대한 일관되지 않은 가정에서 발생하므로 초기 인터페이스 검증은 특히 중요하다.

시뮬레이션(Simulation)은 모든 테스트에서 물리적 하드웨어를 요구하지 않으면서 지속적 테스트를 시스템 동작 수준으로 확장한다. 내비게이션(Navigation), 조작(Manipulation), 이동(Locomotion), 인지(Perception), 임무 로직(Mission Logic)을 반복 가능한 시나리오에서 평가하면서 환경 변수와 장애를 체계적으로 적용할 수 있다. 시뮬레이션이 실제 환경 유효성 확인(Real-World Validation)을 대체하는 것은 아니지만 제한된 로봇 하드웨어나 현장 시설을 사용하기 전에 많은 통합 문제와 동작 회귀(Behavioral Regression)를 발견할 수 있도록 한다.

하드웨어 인 더 루프(Hardware-in-the-Loop, HIL) 테스트는 현실성을 단계적으로 높이는 추가적인 검증 단계를 제공한다. 실제 제어기, 통신 인터페이스, 임베디드 컴퓨터(Embedded Computer) 또는 선택된 장치가 완전한 물리적 배포 전에 시뮬레이션된 플랜트(Plant) 및 환경과 상호작용할 수 있다. HIL은 소프트웨어 전용 테스트만으로 충분히 표현하기 어려우면서도 실제 운용 로봇에서 처음 조사하기에는 비용이 높거나 위험한 타이밍, 통신, 액추에이터 인터페이스, 안전 기능 및 장애 대응을 검증하는 데 특히 유용하다.

지속적 통합(Continuous Integration)은 시프트 레프트 테스트를 확장 가능한 형태로 실행할 수 있게 하는 핵심 메커니즘을 제공한다. 의미 있는 모든 변경사항은 컴파일(Compilation), 정적 검사, 단위 테스트, 선택된 통합 테스트, 커버리지 분석(Coverage Analysis), 패키징(Packaging), 산출물 생성(Artifact Generation)을 자동으로 실행할 수 있다. 더 많은 비용이 필요한 시뮬레이션 또는 HIL 테스트 스위트는 예약된 파이프라인(Scheduled Pipeline)이나 릴리스 후보(Release Candidate)를 대상으로 실행할 수 있다. 따라서 실행 비용에 따라 테스트 빈도를 조정하면서 소프트웨어가 배포 단계에 가까워질수록 점진적으로 더 강력한 검증을 수행할 수 있다.

계층화된 파이프라인(Layered Pipeline)은 비용이 높은 테스트를 시작하기 전에 빠른 피드백을 제공해야 한다. 컴파일, 정적 분석 또는 단위 테스트에서 이미 결함을 발견했다면 동일한 빌드(Build)에 시뮬레이션 클러스터(Simulation Cluster)나 실제 로봇의 시간을 소비할 필요가 없다. 빠른 검사는 느린 테스트 단계로 진입하기 위한 품질 게이트(Quality Gate) 역할을 하며, 성공한 빌드는 통합, 시뮬레이션, HIL, 최종적으로 현장 테스트 단계로 진행한다. 이러한 구조는 테스트 피라미드(Testing Pyramid)의 경제적 원리를 따른다.

위험 기반 테스트(Risk-Based Testing)는 어떤 검사를 가장 이른 시점에 가장 빈번하게 실행해야 하는지를 결정한다. 안전 상태 로직(Safety-State Logic), 모션 허가(Motion Authorization), 감시 타이머(Watchdog), 명령 제한(Command Limit), 위치추정 유효성(Localization Validity), 액추에이터 제어, 장애 처리(Fault Handling)는 실패 시 심각한 결과를 발생시킬 수 있으므로 관련 변경이 있을 때마다 실행할 수 있다. 위험이 낮은 기능은 상대적으로 낮은 빈도로 평가할 수 있다. 따라서 FMEA 결과는 파이프라인 순서, 커버리지 목표(Coverage Target), 장애 주입 시나리오(Fault-Injection Scenario), 릴리스 게이트(Release Gate)에 영향을 줄 수 있다.

지속적 테스트는 재현 가능한 환경(Reproducible Environment)과 통제된 테스트 데이터(Test Data)에도 의존한다. 엔지니어가 장애를 발생시킨 소프트웨어 의존성, 구성, 데이터셋(Dataset), 캘리브레이션(Calibration), 시뮬레이션 월드(Simulation World), 난수 시드(Random Seed), 하드웨어 상태를 재현할 수 없다면 조기에 발견된 장애의 가치가 제한된다. 컨테이너화(Containerization), 버전 관리 구성(Versioned Configuration), 불변 데이터셋(Immutable Dataset), 환경 메타데이터(Environment Metadata), 자동화된 프로비저닝(Automated Provisioning)은 개발자 장비와 CI 인프라에서 생성된 결과를 서로 비교할 수 있도록 지원한다.

AI 기반 로봇 소프트웨어(AI-Enabled Robot Software)에서는 시프트 레프트 원칙을 데이터와 모델 개발 과정까지 확장해야 한다. 데이터셋 검증(Dataset Validation), 전처리 검사(Preprocessing Check), 모델 인터페이스 테스트(Model Interface Test), 텐서 형상 검증(Tensor-Shape Verification), 추론 호환성(Inference Compatibility), 지연시간 측정(Latency Measurement), 기본적인 강건성 검사(Robustness Check)를 시스템 통합 전에 수행할 수 있다. 통계적 성능, 일반화(Generalization), 실제 환경 동작에는 여전히 더 광범위한 평가가 필요하지만 모델이나 데이터셋이 변경될 때 많은 파이프라인 및 통합 결함을 즉시 발견할 수 있다.

회귀 테스트(Regression Testing)는 이전에 발견된 결함을 영구적인 검증 자산(Verification Asset)으로 전환한다. 시뮬레이션, HIL 또는 현장 운용에서 버그(Bug)가 발견되면 엔지니어는 해당 문제를 재현하고 가능한 가장 낮은 테스트 수준에서 자동화 테스트를 생성할 수 있다. 이후 수정된 동작은 향후 동일한 결함이 다시 발생하지 않도록 보호된다. 따라서 시간이 지남에 따라 운용 경험(Operational Experience)이 시프트 레프트 테스트 스위트를 강화하고, 과거에는 개발 후반에 발견되었던 장애를 이후 개발 주기에서는 훨씬 이른 단계에서 발견할 수 있게 한다.

시프트 레프트 테스트를 후반 단계의 유효성 확인(Validation)을 제거하는 방식으로 해석해서는 안 된다. 로봇의 동작은 소프트웨어, 컴퓨팅 자원, 센서, 액추에이터, 네트워크, 사람 및 물리적 환경 사이의 상호작용에서 나타나며 이러한 관계를 초기 테스트만으로 완전히 표현할 수는 없다. 단위 및 통합 테스트는 소프트웨어 신뢰도를 확립하고, 시뮬레이션, HIL, 시스템 테스트(System Testing), 현장 시험(Field Trial), 안전 평가(Safety Evaluation), 벤치마킹(Benchmarking)은 완전한 로봇이 의도된 목적을 충족한다는 점을 점진적으로 더 현실적인 환경에서 입증한다.

지속적 테스트의 지표(Metric)는 단순한 테스트 개수보다 피드백의 품질(Feedback Quality)을 강조해야 한다. 유용한 지표에는 결함 탐지 시간(Time to Detect Defects), 파이프라인 실행시간, 성공 및 실패 추세, 불안정 테스트 비율(Flaky-Test Rate), 커버리지 변화, 테스트 단계에서 발견되지 않고 유출된 결함(Escaped Defect), 회귀 재발률(Regression Recurrence), 장애 위치 식별(Failure Localization) 등이 포함된다. 느리거나 신뢰할 수 없는 피드백을 제공하는 대규모 테스트 스위트는 개발을 방해할 수 있지만 적절하게 계층화된 테스트 스위트는 중요한 문제를 빠르게 발견하면서 비용이 높은 자원을 더 가치 있는 유효성 확인에 사용할 수 있도록 한다.

지속적 테스트는 엔지니어링 책임(Engineering Responsibility)의 방식도 변화시킨다. 테스트는 더 이상 개발 종료 단계에서 별도의 품질팀(Quality Team)만 담당하는 활동이 아니다. 개발자, 시스템 엔지니어(System Engineer), 안전 엔지니어(Safety Engineer), AI 엔지니어, 테스트 엔지니어 및 운영팀(Operations Team)이 명세, 테스트 케이스, 데이터셋, 시나리오, 자동화 및 현장 증거(Field Evidence)에 공동으로 기여한다. 이러한 공동 책임은 테스트 가능성을 아키텍처 품질(Architectural Quality)의 일부로 만들고 검증 증거가 로봇 소프트웨어와 함께 지속적으로 발전하도록 한다.

성숙한 시프트 레프트 전략(Shift-Left Strategy)은 궁극적으로 요구사항에서 구현 및 배포에 이르는 지속적인 증거 체인(Continuous Chain of Evidence)을 구축한다. 각각의 변경사항은 가능한 가장 이른 단계에서 저비용 자동화 검사로 검증되고, 신뢰도가 증가함에 따라 점진적으로 더 현실적인 환경에 노출된다. 로보틱스에서 이러한 접근법은 개발 후반의 통합 문제를 줄이고, 결함 위치 식별을 향상시키며, 제한된 하드웨어 자원을 보호하고, 신뢰할 수 있는 시스템 유효성 확인(System Validation)과 릴리스를 위한 체계적인 기반을 제공한다.

## 01.10. Testing Strategy by Robot Platform AMR Legged UAV

![](images/image10.png){width="7.268055555555556in" height="7.268055555555556in"}

로봇 테스트 전략(Robot Testing Strategy)은 각 플랫폼의 물리적 구조, 이동 메커니즘(Mobility Mechanism), 운용 환경, 자율성 수준(Autonomy Level), 장애 발생 시 결과를 반영해야 한다. 자율이동로봇(Autonomous Mobile Robot, AMR), 다족보행로봇(Legged Robot), 무인항공기(Unmanned Aerial Vehicle, UAV)는 인지(Perception), 위치추정(Localization), 계획(Planning), 제어(Control), 통신(Communication), 진단(Diagnostics)과 같은 공통 소프트웨어 계층을 사용하지만 주요 위험은 크게 다르다. 따라서 공통 소프트웨어 검증과 플랫폼별 시스템 및 현장 유효성 확인(Field Validation)을 결합하는 전략이 필요하다.

공통 소프트웨어 수준에서는 세 플랫폼 모두 정적 분석(Static Analysis), 단위 테스트(Unit Testing), 인터페이스 테스트(Interface Testing), 통합 테스트(Integration Testing), 시뮬레이션(Simulation), 하드웨어 인 더 루프(Hardware-in-the-Loop, HIL), 회귀 테스트(Regression Testing), 통제된 현장 평가(Field Evaluation)를 활용할 수 있다. 수학 함수, 상태 머신(State Machine), 좌표 변환(Coordinate Transformation), 통신 인터페이스, 명령 검증(Command Validation), 장애 처리 로직(Fault-Handling Logic)은 완전한 하드웨어 통합 이전에 테스트해야 한다. 이후 상위 수준 테스트에서는 실제에 가까운 센서, 액추에이터, 동역학(Dynamics), 환경 및 운용 외란(Operational Disturbance)을 점진적으로 추가한다.

자율이동로봇(AMR)은 주로 바퀴와 지면의 상호작용(Wheel-Ground Interaction)에 의해 움직임이 제한되는 지지면 위에서 운용된다. 따라서 테스트 전략은 위치추정 정확도, 지도 일관성(Map Consistency), 장애물 감지, 경로 계획(Path Planning), 궤적 추종(Trajectory Tracking), 정지 동작, 도킹(Docking), 교통 상호작용(Traffic Interaction), 사람 주변에서의 안전한 주행에 중점을 둔다. 실내 AMR은 좁은 통로, 교차로, 문, 엘리베이터, 반사 표면, 동적 장애물(Dynamic Obstacle), 변화하는 시설 배치에 대한 광범위한 평가가 추가로 필요하다.

AMR 위치추정 테스트(Localization Testing)는 정상 상태의 정확도뿐만 아니라 성능 저하 상황도 포함해야 한다. 랜드마크(Landmark) 누락, LiDAR 가림(Occlusion), 반복적인 복도 구조, 휠 슬립(Wheel Slip), 지도 변경, 임시 장애물 또는 열악한 시각 조건을 적용하여 위치추정 신뢰도와 복구 메커니즘(Recovery Mechanism)이 올바르게 동작하는지 확인할 수 있다. 내비게이션 소프트웨어(Navigation Software)는 단순히 목적지에 도달하는 것뿐만 아니라 자세 불확실성(Pose Uncertainty)이 허용할 수 없는 수준에 도달했음을 인식하고 필요에 따라 복구, 감속 운용 또는 안전 정지(Safe Stop) 상태로 전환할 수 있어야 한다.

장애물 회피(Obstacle Avoidance)와 안전구역 동작(Safety-Zone Behavior)은 AMR이 작업자 및 시설과 가까운 거리에서 운용되는 경우가 많기 때문에 핵심 테스트 영역이다. 시나리오에서는 장애물 크기, 접근 방향, 상대속도, 센서 가시성(Sensor Visibility), 로봇 속도, 페이로드(Payload), 정지거리를 다양하게 변화시켜야 한다. 테스트에서는 일반적인 경로 계획 동작과 독립적인 안전 기능(Safety Function)을 구분하고, 통신 또는 계획 기능의 장애가 모션 억제(Motion Inhibition), 비상 정지(Emergency Stop) 또는 기타 보호 메커니즘을 우회하지 못하는지 검증해야 한다.

AMR 플릿 운용(Fleet Operation)은 추가적인 분산 시스템 테스트(Distributed-System Testing)를 요구한다. 여러 로봇이 교차로, 충전 스테이션(Charging Station), 엘리베이터, 좁은 통로 또는 임무 자원을 동시에 사용하려 할 수 있다. 테스트에서는 교통 교착상태(Traffic Deadlock), 지연된 플릿 명령, 네트워크 단절, 중복 임무, 지도 버전 불일치, 서버 재시작, 통신 손실 이후의 복구를 평가해야 한다. 장시간 테스트(Long-Duration Testing)는 메모리 증가, 누적 위치추정 오차, 충전 실패, 스케줄링 불안정성(Scheduling Instability)을 발견하는 데도 중요하다.

다족보행로봇(Legged Robot)은 이동이 동적 균형(Dynamic Balance)과 반복적인 접촉 전환(Contact Transition)에 의존하므로 상당히 다른 검증 과제를 가진다. 테스트에서는 상태 추정(State Estimation), 보행 생성(Gait Generation), 발 배치(Foot Placement), 접촉 감지(Contact Detection), 전신 제어(Whole-Body Control), 관절 제한(Joint Limit), 액추에이터 토크(Actuator Torque), 지형 적응(Terrain Adaptation), 낙상 대응(Fall Handling)을 다루어야 한다. AMR에서는 작은 추종 오차로 끝날 수 있는 오류도 다족보행 플랫폼에서는 불안정성을 유발하여 빠르게 자세를 완전히 상실하게 만들 수 있다.

시뮬레이션은 실제 하드웨어를 반복적으로 손상시키지 않고 많은 낙상, 외란 및 지형 변화를 평가할 수 있기 때문에 다족보행로봇 테스트에서 특히 높은 가치를 가진다. 테스트에서는 마찰(Friction), 경사면, 계단, 디딤돌(Stepping Stone), 유연한 표면(Compliant Surface), 외부 밀침(External Push), 페이로드 분포, 센서 노이즈(Sensor Noise)를 변화시킬 수 있다. 시뮬레이션은 정상 보행과 복구 동작을 모두 시험해야 하지만 접촉 동역학(Contact Dynamics)과 액추에이터 특성이 실제 로봇과 다를 수 있다는 점을 고려해야 한다.

다족보행로봇의 실제 테스트(Physical Testing)는 난이도를 점진적으로 높이는 방식으로 수행해야 한다. 초기 시험에서는 지지 구조물(Support Structure), 낮은 속도, 제한된 작업공간, 보수적인 토크 또는 모션 제한을 적용한 후 자유 보행(Free Locomotion)과 더 강한 외란을 점차 도입할 수 있다. 낙상 감지(Fall Detection), 보호 정지(Protective Shutdown), 액추에이터 장애 처리, 열 한계(Thermal Limit), 관절 한계 보호(Joint-Limit Protection), 비상 정지 동작은 장애 발생 시 로봇 손상이나 주변 작업자의 위험으로 이어질 수 있으므로 명시적인 검증이 필요하다.

조작(Manipulation)을 수행하는 다족보행로봇은 상체 동작이 균형과 접촉력(Contact Force)을 변화시키기 때문에 이동과 조작을 결합한 테스트가 필요하다. 뻗기(Reaching), 운반(Carrying), 밀기(Pushing), 당기기(Pulling), 양팔 사용은 전체 시스템의 질량중심(Center of Mass)과 운동량(Momentum)을 변화시킨다. 따라서 보행과 조작을 완전히 독립된 기능으로만 검증하기보다 다양한 페이로드, 지지 구성(Support Configuration), 접촉 전환 및 외란 조건에서 전신 협응(Whole-Body Coordination)을 평가해야 한다.

무인항공기(UAV)는 제어 상실이 통제되지 않은 3차원 운동과 충돌로 이어질 수 있기 때문에 또 다른 위험 특성을 가진다. 따라서 테스트에서는 비행 제어 안정성(Flight-Control Stability), 상태 추정, 항법(Navigation), 추진(Propulsion), 통신, 지오펜싱(Geofencing), 임무 관리(Mission Management), 에너지 상태, 이중화(Redundancy), 비상 동작(Emergency Behavior)을 중점적으로 검증한다. 타이밍 오류나 잘못된 명령은 비행 중 빠르게 안전 관련 문제로 발전할 수 있으므로 소프트웨어 검증을 기체 동역학(Vehicle Dynamics)과 긴밀하게 연결해야 한다.

UAV 테스트는 소프트웨어 전용 시뮬레이션에서 HIL을 거쳐 신중하게 통제된 실제 비행 테스트(Flight Test)로 발전해야 한다. 시뮬레이션에서는 유도(Guidance), 항법, 임무 로직, 바람 외란(Wind Disturbance), 센서 장애 및 대규모 시나리오 집합을 평가할 수 있다. HIL에서는 실제 비행 컴퓨터(Flight Computer)와 통신 인터페이스를 실시간 기체 모델(Real-Time Vehicle Model)에 연결하여 실제 비행에서 동일한 조건에 기체를 노출하기 전에 타이밍, 오토파일럿(Autopilot) 동작, 입출력(I/O), 장애 대응을 검증할 수 있다.

UAV 상태 추정 테스트(State-Estimation Testing)에는 GNSS 성능 저하 또는 상실, IMU 이상, 자력계 교란(Magnetometer Disturbance), 기압계 오류(Barometric Error), 시각 항법 성능 저하(Visual-Navigation Degradation), 센서 측정값 불일치를 포함해야 한다. 항법 신뢰도(Navigation Confidence)가 저하될 때 시스템은 정의된 동작을 수행해야 한다. 임무와 아키텍처에 따라 추정 정보원 전환, 운용 제한, 위치 유지(Hold Position), 복귀(Return), 착륙(Landing) 또는 사전에 정의된 다른 비상 상태(Contingency State)로의 전환이 포함될 수 있다.

추진 및 에너지 관리(Propulsion and Energy Management)는 남아 있는 비행 능력이 사용 가능한 추력(Thrust)과 배터리 상태에 직접적으로 의존하므로 UAV에서 명시적으로 검증해야 한다. 테스트에서는 배터리 부족, 전압 강하(Voltage Sag), 추진 성능 저하, 예상하지 못한 에너지 소비, 페이로드 변화, 비행 지속시간 한계(Endurance Limit)에 가까운 임무 의사결정을 평가해야 한다. 장애 시나리오에서는 제어 권한(Control Authority)이나 사용 가능한 에너지가 부족해지기 전에 기체가 성능 저하를 감지하고 의도된 비상 동작을 실행할 수 있는지 검증해야 한다.

통신 손실 테스트(Communication-Loss Testing)는 플랫폼별로 차이가 있지만 원격 감독(Remote Supervision)을 받는 UAV 운용에서는 특히 중요하다. 기체는 즉각적인 안정화를 위해 지속적인 통신 연결에 의존해서는 안 되며 명령 또는 텔레메트리 링크(Telemetry Link)가 상실되었을 때의 임무 수준 대응은 결정론적이고 검증되어야 한다. 동일한 원칙이 AMR과 다족보행로봇에도 적용되지만 지상 로봇은 일반적으로 현재 위치에서 정지할 수 있는 반면 공중 플랫폼은 계속 능동적인 제어(Active Control)를 수행해야 하므로 안전 상태가 서로 다를 수 있다.

환경 테스트(Environmental Testing) 역시 플랫폼별 노출 조건을 반영해야 한다. AMR은 바닥 오염, 경사로, 조명 변화, 먼지, 좁은 공간, 보행자 통행을 경험할 수 있다. 다족보행로봇은 불규칙한 지형, 불확실한 접촉, 충격 및 빠른 하중 재분배(Load Redistribution)를 경험한다. UAV는 바람, 난류(Turbulence), 진동, 온도 변화, 강수 조건, 전자기 간섭(Electromagnetic Interference), 변화하는 GNSS 조건의 영향을 받는다. 테스트 시나리오는 각 플랫폼의 센싱과 제어에 실질적으로 영향을 미치는 환경 요인을 재현해야 한다.

AI 기반 기능(AI-Enabled Function)은 기존 소프트웨어 테스트와 함께 플랫폼별 시나리오 커버리지(Scenario Coverage)를 요구한다. AMR 인지 모델(Perception Model)은 다양한 보행자, 팔레트(Pallet), 복도 및 바닥 조건을 포함해야 하며, 다족보행로봇 정책(Policy)은 지형, 접촉 및 외란의 다양성을 고려해야 한다. UAV 인지 시스템은 고도, 시점(Viewpoint), 날씨, 배경 및 표적 변화(Target Variation)를 포함해야 한다. 의사결정이 사용되는 실제 운용 조건을 평가에 반영하지 않는다면 모델 정확도만으로는 충분하지 않다.

위험 기반 테스트(Risk-Based Testing)는 각 플랫폼 기능을 어느 정도 깊이까지 평가해야 하는지를 결정하기 위한 공통 프레임워크(Framework)를 제공한다. 고장 형태 및 영향 분석(Failure Mode and Effects Analysis, FMEA)을 사용하면 플랫폼별 고장 형태를 단위, 통합, 시뮬레이션, HIL 및 현장 테스트와 연결할 수 있다. AMR의 모션 허가, 다족보행로봇의 균형 보호(Balance Protection), UAV의 비행 제어 및 비상 로직과 같이 결과가 심각할 수 있는 동작에는 영향이 제한적인 기능보다 더 강한 커버리지, 장애 주입(Fault Injection), 추적성(Traceability), 회귀 보호(Regression Protection)를 적용해야 한다.

현장 유효성 확인(Field Validation)은 서로 분리된 기술적 시연이 아니라 대표적인 임무(Representative Mission)를 재현해야 한다. AMR은 실제적인 운송 또는 서비스 워크플로를 완료해야 하고, 다족보행로봇은 대표적인 지형과 객체를 이동하고 상호작용해야 하며, UAV는 정의된 운용 조건에서 완전한 비행 임무를 수행해야 한다. 임무 수준 테스트(Mission-Level Testing)는 구성요소 테스트만으로 완전히 재현하기 어려운 인지, 계획, 제어, 통신, 에너지 관리, 운영자 및 환경 불확실성 사이의 상호작용을 드러낸다.

세 플랫폼의 차이에도 불구하고 모두 동일한 점진적 테스트 철학(Progressive Testing Philosophy)의 이점을 얻을 수 있다. 비용이 낮은 소프트웨어 결함을 초기 단계에서 발견하고, 완전한 통합 전에 인터페이스를 평가하며, 시뮬레이션을 사용하여 광범위한 시나리오 공간(Scenario Space)을 탐색하고, 실제 하드웨어 동작이 중요한 경우 HIL을 적용하며, 실제 동역학과 환경이 필요한 문제에 대해서만 물리적 테스트를 수행한다. 테스트 증거(Test Evidence)는 요구사항, 위험, 소프트웨어 버전, 구성, 데이터셋 및 플랫폼 상태까지 추적할 수 있어야 한다.

따라서 성숙한 플랫폼별 테스트 전략(Platform-Specific Testing Strategy)은 완전히 분리된 세 가지 테스트 체계를 만드는 것이 아니다. 공통된 검증 기반(Verification Foundation)을 구축하고 각 로봇의 물리적 동작과 주요 위험에 따라 상위 테스트 계층을 조정하는 것이다. AMR은 내비게이션과 사람과 공유하는 지상 환경에서의 운용을 강조하고, 다족보행로봇은 균형과 접촉이 많은 동역학(Contact-Rich Dynamics)을 강조하며, UAV는 비행 안정성과 공중 비상 상황(Airborne Contingency)을 강조한다. 동시에 세 플랫폼 모두 체계적인 소프트웨어 검증과 점진적으로 현실성을 높이는 유효성 확인에 의존한다.
