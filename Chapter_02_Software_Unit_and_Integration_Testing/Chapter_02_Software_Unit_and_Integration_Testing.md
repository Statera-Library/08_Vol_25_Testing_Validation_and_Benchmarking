**Volume 25. Testing Validation and Benchmarking**


# Chapter 02. Software Unit and Integration Testing

##  

## 02.01. Unit Testing Frameworks GTest Catch2 PyTest [w/Code]

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

Unit testing provides the first executable verification layer for robotics software by checking individual functions, classes, algorithms, and software components in isolation. Within a broader software unit and integration testing strategy, frameworks such as GoogleTest, Catch2, and PyTest provide repeatable mechanisms for expressing expected behavior, detecting regressions, and producing machine-readable results that can later be incorporated into automated integration and CI pipelines.

GoogleTest, commonly called GTest, is widely used for C++ robotics software because it supports assertions, test fixtures, parameterized tests, typed tests, and structured test execution. A typical test creates controlled inputs, invokes the unit under test, and compares the observed result with an expected value using assertions such as EXPECT_EQ, EXPECT_NEAR, or ASSERT_TRUE. This pattern works well for deterministic mathematical and control-oriented components.

Test fixtures in GoogleTest are particularly useful when multiple tests require the same initialization procedure. A fixture can construct controller objects, initialize configuration parameters, allocate representative sensor messages, or prepare synthetic robot states before each test executes. Setup and teardown logic therefore remains separate from individual test intentions, reducing duplication and helping engineers maintain consistent initial conditions across a large regression suite.

Parameterized testing extends this approach by executing the same test logic over many input combinations. A velocity limiter, coordinate transformation, kinematic solver, trajectory interpolator, or safety threshold function can be evaluated against normal values, boundary conditions, invalid inputs, and extreme operating cases without duplicating test code. For robotics systems, this technique is valuable because physical behavior often depends on continuous variables with many important boundary regions.

Catch2 provides another C++ testing approach with a compact syntax and relatively low configuration overhead. Its TEST_CASE and SECTION concepts allow related behaviors to be expressed in readable test structures, while REQUIRE and CHECK assertions distinguish between conditions that must terminate a test path and conditions that may permit additional checks. Catch2 can therefore be attractive for libraries or algorithm modules where developers want tests to remain close to ordinary C++ expressions.

The choice between GoogleTest and Catch2 should normally follow the surrounding build environment, dependency policy, team conventions, and existing test infrastructure rather than syntax preference alone. GoogleTest is often suitable for large C++ projects with established fixtures and extensive automation, while Catch2 can provide concise organization for smaller libraries and focused components. Consistency across a robotics codebase is generally more valuable than mixing frameworks without a clear engineering reason.

PyTest serves a similar role for Python components but uses Python\'s dynamic language features to make test construction highly concise. Test discovery can identify appropriately named test files and functions automatically, while ordinary assert expressions express expected behavior without specialized assertion macros. This makes PyTest useful for robot orchestration logic, data processing utilities, AI preprocessing code, configuration validation, service clients, and other Python-based subsystems.

PyTest fixtures provide reusable initialization and dependency management for tests. A fixture may generate synthetic sensor observations, create temporary configuration files, initialize mock interfaces, prepare sample inference tensors, or establish temporary data directories. Fixtures can be scoped according to function, class, module, or session requirements, allowing expensive setup operations to be shared when appropriate while preserving isolation for state-sensitive software components.

A robust robotics unit test should isolate the software unit from physical hardware and external services whenever possible. Motor drivers, cameras, LiDAR devices, databases, networks, clocks, and remote APIs introduce nondeterminism and operational dependencies that make failures difficult to reproduce. Their behavior should instead be represented through controlled interfaces, test doubles, or deterministic inputs, leaving hardware-dependent verification to later integration, simulation, and HIL stages.

Determinism is especially important for control and estimation algorithms. Tests should define explicit initial states, timestamps, parameters, coordinate frames, and numerical tolerances so that repeated execution produces equivalent conclusions. Floating-point calculations should usually be compared using tolerances rather than exact equality. A kinematic transformation, PID calculation, filter update, or trajectory sample can then be validated against analytically derived or previously verified reference results.

Boundary and failure conditions deserve the same attention as nominal behavior. A unit test suite should examine empty inputs, maximum and minimum values, invalid configuration parameters, unavailable data, numerical singularities, NaN values, timeout conditions, and unexpected state transitions where applicable. Robotics software interacts continuously with imperfect sensors and changing environments, so software that succeeds only with ideal inputs cannot be considered adequately verified.

Test organization should mirror software architecture closely enough that failures can be localized rapidly. Tests can be grouped around libraries, classes, algorithms, or component responsibilities, with names describing the behavior being verified rather than implementation details. When a regression occurs, a descriptive test such as rejecting an invalid joint limit communicates more diagnostic information than a generic identifier, reducing the time required to understand the affected requirement and code path.

Unit tests should also remain independent of execution order. One test must not rely on state created accidentally by another test, because parallel execution, selective execution, or CI sharding can change ordering. Mutable global state should therefore be minimized or reset explicitly. Temporary files and generated resources should be isolated and cleaned automatically so that local development, container execution, and continuous integration environments produce comparable results.

Performance-sensitive robot functions can include lightweight timing checks, but unit tests should distinguish functional correctness from formal performance benchmarking. A test can detect a severe computational regression in a frequently executed routine, yet execution time varies with processors, operating systems, scheduling, and CI load. Strict real-time latency requirements are better verified under controlled integration, real-time, HIL, or benchmark environments designed for timing measurements.

The three frameworks can coexist in a heterogeneous robot platform when language boundaries require it. A C++ motion-control library may use GoogleTest, a compact C++ utility library may use Catch2, and Python perception utilities may use PyTest. The important architectural objective is to normalize how these suites are invoked and reported so that developers receive a unified pass/fail view despite differences in implementation language and framework conventions.

Automation turns individual tests into an engineering quality gate. Build systems and CI pipelines should execute unit tests whenever relevant source code changes, capture failure logs, preserve test reports, and reject changes that violate defined quality criteria. Because Chapter 02 progresses from framework-level unit testing toward mocking, ROS 2 testing, controller and perception tests, integration tests, APIs, data pipelines, and CI integration, unit frameworks form the foundation for progressively broader verification.

Effective unit testing is ultimately less about maximizing the number of test cases than about establishing fast, deterministic evidence that software components satisfy their intended contracts. GoogleTest, Catch2, and PyTest provide different language-specific mechanisms for building that evidence, but the core discipline remains consistent: isolate behavior, control inputs, define observable expectations, exercise boundaries, report failures clearly, and run the suite continuously as the robot software evolves.

단위 테스트(Unit Testing)는 개별 함수, 클래스, 알고리즘 및 소프트웨어 구성요소(Component)를 격리된 상태에서 검사하여 로보틱스 소프트웨어(Robotics Software)의 첫 번째 실행 가능한 검증 계층을 제공한다. 광범위한 소프트웨어 단위 및 통합 테스트(Software Unit and Integration Testing) 전략에서 GoogleTest, Catch2, PyTest와 같은 프레임워크(Framework)는 예상 동작을 표현하고, 회귀(Regression)를 탐지하며, 이후 자동화된 통합 및 지속적 통합(CI, Continuous Integration) 파이프라인에 포함할 수 있는 기계 판독형 결과를 생성하는 반복 가능한 방법을 제공한다.

일반적으로 GTest라고 불리는 GoogleTest는 어설션(Assertion), 테스트 픽스처(Test Fixture), 매개변수화 테스트(Parameterized Test), 타입 테스트(Typed Test), 구조화된 테스트 실행을 지원하기 때문에 C++ 기반 로보틱스 소프트웨어에서 널리 사용된다. 일반적인 테스트는 제어된 입력을 생성하고, 테스트 대상 단위(Unit Under Test)를 실행한 후, EXPECT_EQ, EXPECT_NEAR, ASSERT_TRUE와 같은 어설션을 사용하여 관측된 결과와 예상값을 비교한다. 이러한 패턴은 결정론적 수학 및 제어 중심 구성요소를 검증하는 데 적합하다.

GoogleTest의 테스트 픽스처(Test Fixture)는 여러 테스트가 동일한 초기화 절차를 필요로 할 때 특히 유용하다. 픽스처는 각 테스트가 실행되기 전에 제어기(Controller) 객체를 생성하고, 구성 매개변수를 초기화하며, 대표적인 센서 메시지를 할당하거나 합성 로봇 상태(Synthetic Robot State)를 준비할 수 있다. 따라서 설정(Setup) 및 정리(Teardown) 로직을 개별 테스트 목적과 분리할 수 있어 코드 중복을 줄이고 대규모 회귀 테스트 스위트(Regression Test Suite) 전체에서 일관된 초기 조건을 유지할 수 있다.

매개변수화 테스트(Parameterized Testing)는 동일한 테스트 로직을 다양한 입력 조합에 반복 실행하는 방식으로 이러한 접근법을 확장한다. 속도 제한기(Velocity Limiter), 좌표 변환(Coordinate Transformation), 운동학 해석기(Kinematic Solver), 궤적 보간기(Trajectory Interpolator), 안전 임계값 함수(Safety Threshold Function)를 정상값, 경계 조건, 잘못된 입력 및 극단적인 운용 조건에 대해 중복된 테스트 코드 없이 평가할 수 있다. 로보틱스 시스템은 물리적 동작이 수많은 중요 경계 영역을 가진 연속 변수에 의존하므로 이러한 기법의 가치가 크다.

Catch2는 간결한 문법과 비교적 낮은 구성 부담을 제공하는 또 다른 C++ 테스트 접근법이다. TEST_CASE와 SECTION 개념을 사용하여 관련 동작을 읽기 쉬운 테스트 구조로 표현할 수 있으며, REQUIRE와 CHECK 어설션은 테스트 경로를 즉시 종료해야 하는 조건과 이후 검사를 계속할 수 있는 조건을 구분한다. 따라서 Catch2는 개발자가 테스트를 일반적인 C++ 표현식과 가깝게 유지하려는 라이브러리 또는 알고리즘 모듈에 적합할 수 있다.

GoogleTest와 Catch2 중 어떤 것을 선택할지는 단순한 문법 선호보다는 주변 빌드 환경(Build Environment), 의존성 정책(Dependency Policy), 팀 규칙 및 기존 테스트 인프라(Test Infrastructure)를 기준으로 결정하는 것이 바람직하다. GoogleTest는 확립된 픽스처와 광범위한 자동화가 존재하는 대규모 C++ 프로젝트에 적합한 경우가 많으며, Catch2는 소규모 라이브러리와 집중된 구성요소에 간결한 구성을 제공할 수 있다. 명확한 공학적 이유 없이 여러 프레임워크를 혼합하는 것보다 로보틱스 코드베이스(Robotics Codebase) 전체의 일관성을 유지하는 것이 일반적으로 더 중요하다.

PyTest는 Python 구성요소에서 유사한 역할을 수행하지만, Python의 동적 언어 기능(Dynamic Language Feature)을 활용하여 테스트 작성을 매우 간결하게 만든다. 테스트 탐색(Test Discovery)은 적절하게 명명된 테스트 파일과 함수를 자동으로 식별할 수 있으며, 일반적인 assert 표현식으로 별도의 특수 어설션 매크로 없이 예상 동작을 표현할 수 있다. 이러한 특성으로 PyTest는 로봇 오케스트레이션 로직(Robot Orchestration Logic), 데이터 처리 유틸리티, AI 전처리 코드, 구성 검증 및 서비스 클라이언트(Service Client)와 같은 Python 기반 하위 시스템에 유용하다.

PyTest 픽스처(PyTest Fixture)는 테스트를 위한 재사용 가능한 초기화 및 의존성 관리를 제공한다. 픽스처는 합성 센서 관측값(Synthetic Sensor Observation)을 생성하거나, 임시 구성 파일을 만들고, 모의 인터페이스(Mock Interface)를 초기화하며, 샘플 추론 텐서(Inference Tensor)를 준비하거나 임시 데이터 디렉터리를 구성할 수 있다. 픽스처의 범위는 함수(Function), 클래스(Class), 모듈(Module), 세션(Session) 단위로 설정할 수 있으므로 필요한 경우 비용이 큰 초기화 작업을 공유하면서 상태에 민감한 소프트웨어 구성요소의 격리성을 유지할 수 있다.

견고한 로보틱스 단위 테스트(Robotics Unit Test)는 가능한 경우 소프트웨어 단위를 물리적 하드웨어와 외부 서비스로부터 격리해야 한다. 모터 드라이버(Motor Driver), 카메라(Camera), 라이다(LiDAR), 데이터베이스(Database), 네트워크(Network), 시계(Clock), 원격 API는 비결정성과 운용 의존성을 유발하여 실패의 재현을 어렵게 만들 수 있다. 따라서 이러한 요소의 동작은 제어된 인터페이스, 테스트 대역(Test Double), 결정론적 입력으로 표현하고, 하드웨어 의존 검증은 이후 통합(Integration), 시뮬레이션(Simulation), HIL(Hardware-in-the-Loop) 단계에서 수행하는 것이 적절하다.

결정성(Determinism)은 특히 제어 및 상태 추정 알고리즘(Control and Estimation Algorithm)에서 중요하다. 테스트는 명시적인 초기 상태, 타임스탬프(Timestamp), 매개변수, 좌표 프레임(Coordinate Frame), 수치 허용오차(Numerical Tolerance)를 정의하여 반복 실행에서도 동등한 결론을 얻을 수 있도록 해야 한다. 부동소수점 계산(Floating-Point Calculation)은 일반적으로 정확한 동일성보다 허용오차를 이용하여 비교해야 한다. 이를 통해 운동학 변환, PID 계산, 필터 갱신(Filter Update), 궤적 샘플을 해석적으로 도출되거나 사전에 검증된 기준 결과와 비교할 수 있다.

경계 및 실패 조건(Boundary and Failure Condition)은 정상 동작과 동일한 수준의 주의를 기울여야 한다. 단위 테스트 스위트(Unit Test Suite)는 해당되는 경우 빈 입력, 최댓값과 최솟값, 잘못된 구성 매개변수, 사용할 수 없는 데이터, 수치적 특이점(Numerical Singularity), NaN 값, 타임아웃(Timeout), 예상하지 못한 상태 전이(State Transition)를 검사해야 한다. 로보틱스 소프트웨어는 불완전한 센서와 지속적으로 변화하는 환경과 상호작용하므로 이상적인 입력에서만 성공하는 소프트웨어는 충분히 검증되었다고 볼 수 없다.

테스트 구성(Test Organization)은 실패 원인을 빠르게 국소화할 수 있을 정도로 소프트웨어 아키텍처(Software Architecture)를 밀접하게 반영해야 한다. 테스트는 라이브러리, 클래스, 알고리즘 또는 구성요소의 책임을 중심으로 그룹화할 수 있으며, 이름은 구현 세부사항보다 검증하려는 동작을 설명하도록 작성하는 것이 바람직하다. 회귀 문제가 발생했을 때 \'잘못된 관절 제한값 거부\'와 같이 설명적인 테스트 이름은 일반적인 식별자보다 더 많은 진단 정보를 제공하여 영향을 받은 요구사항과 코드 경로를 파악하는 시간을 줄여준다.

단위 테스트는 실행 순서와도 독립적이어야 한다. 하나의 테스트가 다른 테스트에서 우연히 생성된 상태에 의존해서는 안 된다. 병렬 실행(Parallel Execution), 선택적 실행(Selective Execution), 지속적 통합 분할(CI Sharding) 과정에서 테스트 실행 순서가 달라질 수 있기 때문이다. 따라서 변경 가능한 전역 상태(Mutable Global State)는 최소화하거나 명시적으로 초기화해야 한다. 임시 파일과 생성된 리소스도 격리하고 자동으로 정리하여 로컬 개발 환경, 컨테이너(Container) 실행 환경, 지속적 통합 환경에서 서로 비교 가능한 결과가 생성되도록 해야 한다.

성능에 민감한 로봇 함수에는 가벼운 실행 시간 검사를 포함할 수 있지만, 단위 테스트에서는 기능적 정확성(Functional Correctness)과 공식적인 성능 벤치마킹(Performance Benchmarking)을 구분해야 한다. 테스트를 통해 빈번하게 실행되는 루틴의 심각한 계산 성능 저하를 탐지할 수 있지만 실행 시간은 프로세서, 운영체제, 스케줄링(Scheduling), CI 부하에 따라 달라진다. 엄격한 실시간 지연시간(Real-Time Latency) 요구사항은 타이밍 측정을 위해 설계된 통제된 통합, 실시간, HIL 또는 벤치마크 환경에서 검증하는 것이 적절하다.

언어 경계(Language Boundary)로 인해 필요한 경우 세 가지 프레임워크는 이기종 로봇 플랫폼(Heterogeneous Robot Platform)에서 함께 사용할 수 있다. C++ 모션 제어 라이브러리는 GoogleTest를 사용하고, 소규모 C++ 유틸리티 라이브러리는 Catch2를 사용하며, Python 기반 인지 유틸리티는 PyTest를 사용할 수 있다. 중요한 아키텍처 목표는 구현 언어와 프레임워크 규칙이 서로 다르더라도 이러한 테스트 스위트의 실행 및 결과 보고 방식을 표준화하여 개발자에게 통합된 성공/실패(Pass/Fail) 관점을 제공하는 것이다.

자동화(Automation)는 개별 테스트를 공학적 품질 게이트(Quality Gate)로 전환한다. 빌드 시스템(Build System)과 지속적 통합 파이프라인(CI Pipeline)은 관련 소스 코드가 변경될 때마다 단위 테스트를 실행하고, 실패 로그(Failure Log)를 수집하며, 테스트 보고서를 보존하고, 정의된 품질 기준을 위반하는 변경사항을 거부해야 한다. 프레임워크 수준의 단위 테스트에서 모킹(Mocking), ROS 2 테스트, 제어기 및 인지 테스트, 통합 테스트, API, 데이터 파이프라인, CI 통합으로 검증 범위가 확장되므로 단위 테스트 프레임워크는 점진적으로 확대되는 소프트웨어 검증 체계의 기반을 형성한다.

효과적인 단위 테스트의 핵심은 단순히 테스트 사례(Test Case)의 수를 최대화하는 것이 아니라 소프트웨어 구성요소가 의도된 계약(Contract)을 충족한다는 빠르고 결정론적인 증거를 확립하는 데 있다. GoogleTest, Catch2, PyTest는 이러한 증거를 구축하기 위한 서로 다른 언어별 메커니즘을 제공하지만 핵심 원칙은 동일하다. 동작을 격리하고, 입력을 제어하며, 관측 가능한 기대 결과를 정의하고, 경계 조건을 검사하며, 실패를 명확하게 보고하고, 로봇 소프트웨어가 발전하는 전체 과정에서 테스트 스위트를 지속적으로 실행해야 한다.

##  

## 02.02. Mocking and Stubbing for Robot HW Dependencies [w/Code]

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

Robotics software frequently depends on physical devices that are unavailable, expensive, slow, nondeterministic, or unsafe to operate during routine software testing. Motors, encoders, cameras, LiDAR sensors, IMUs, GNSS receivers, battery controllers, and safety devices can therefore prevent conventional unit tests from remaining fast and repeatable. Mocking and stubbing replace these hardware dependencies with controlled software representations so individual components can be verified independently.

A hardware abstraction boundary is the foundation of effective mocking. Instead of allowing control or perception algorithms to communicate directly with a device driver, the software exposes an interface describing operations such as reading encoder positions, obtaining IMU measurements, sending motor commands, or checking device status. Production code connects this interface to real hardware, while unit tests substitute a mock or stub implementation without changing the component being tested.

A stub provides predetermined responses to requests from the software under test. For example, an encoder stub may always return a known wheel position, an IMU stub may provide a predefined acceleration vector, and a battery stub may report a fixed state of charge. Stubs are especially useful when the purpose of the test is to control input conditions rather than verify detailed interactions between the tested component and its dependency.

Mocks extend this concept by recording or validating interactions. A mock motor interface can verify that a controller issued a specific torque command, that an emergency condition resulted in a zero-velocity request, or that initialization invoked device configuration in the required sequence. Tests can define expectations for function arguments, invocation counts, return values, and error behavior, allowing both computational results and communication contracts to be verified.

Dependency injection makes these substitutions practical. A robot component can receive a hardware interface through its constructor, initialization function, or configuration mechanism rather than constructing a concrete hardware driver internally. During normal operation, the real implementation is injected; during testing, a mock implementation is supplied. This design reduces coupling between algorithm logic and device-specific code while improving testability and architectural modularity.

C++ robotics projects can combine interface-oriented design with mocking facilities such as Google Mock. A virtual hardware interface may define methods such as readPosition(), readVelocity(), setTorque(), or getStatus(), while a mock class implements corresponding mock methods. The test then configures expected calls and return values before executing the controller, enabling hardware-facing behavior to be examined without connecting an actual actuator or sensor.

Python software can achieve similar isolation through mock objects, monkeypatching, fixtures, or lightweight fake classes. A test may replace a camera API with a function returning a synthetic frame or substitute a network-connected sensor client with an object that generates deterministic messages. PyTest fixtures can package these replacements so the same simulated dependency is reused consistently across related test cases while remaining isolated from production resources.

Mocking becomes particularly important when testing failure handling. Real hardware failures are often difficult or undesirable to reproduce deliberately, whereas a mock can generate them deterministically. A sensor interface can raise a communication error, return stale timestamps, report invalid measurements, or simulate a disconnected device. A motor driver mock can reject commands or report an overtemperature state, allowing recovery and fault-management logic to be exercised safely.

Timing-related dependencies also require careful treatment. Robot software often uses clocks, timers, watchdogs, and timeout mechanisms that would make tests unnecessarily slow if they depended on wall-clock time. A mock clock can advance time programmatically, enabling a test to verify a 500 ms timeout or multi-second watchdog transition almost instantly. Controlling time also eliminates scheduling variations that might otherwise create intermittent and difficult-to-reproduce test failures.

Sensor stubs should represent meaningful physical conditions rather than arbitrary values. An IMU test sequence might represent a stationary robot, constant angular motion, or a sudden disturbance, while encoder values may describe forward travel or wheel slip. By constructing inputs around recognizable operating conditions, developers can relate test failures to expected robot behavior and build reusable datasets for algorithm-level regression testing.

Actuator mocking focuses primarily on commands and safety constraints because no physical motion occurs. Tests can confirm that velocity, current, torque, steering angle, or joint-position commands remain within configured limits. They can also verify that invalid state estimates, communication failures, or safety events suppress normal commands. This approach provides early evidence that software respects command contracts before the same logic is connected to real actuators.

Mocks should not reproduce every internal detail of the real device. Excessively detailed mocks can become alternative implementations of the hardware driver and may duplicate its defects or assumptions. A better design models only the externally observable contract required by the software under test. When realistic device dynamics or protocol behavior becomes necessary, testing should progressively move toward simulation, software integration, or hardware-in-the-loop environments.

Stubs, mocks, fakes, and simulators therefore serve different verification purposes. A stub supplies controlled data, a mock verifies interactions, and a fake may provide a simplified but functional implementation such as an in-memory device service. A simulator represents physical or temporal behavior at greater fidelity. Selecting the smallest test double that satisfies the verification objective keeps unit tests understandable, deterministic, and computationally inexpensive.

Test doubles must also reproduce abnormal boundary conditions that are difficult to obtain with healthy hardware. These include saturated sensor values, packet loss, delayed responses, invalid checksums, repeated timestamps, encoder rollover, intermittent connectivity, and initialization failures. Systematically injecting such conditions helps determine whether robot software transitions to defined degraded or safe states rather than propagating corrupted data or uncontrolled commands.

The boundary between mocking and integration testing should remain explicit. A controller tested against a mock motor driver demonstrates that the controller uses the driver interface correctly, but it does not prove that the production driver communicates correctly with the physical motor. That evidence must come from higher test levels. The testing structure therefore progresses from isolated software dependencies toward ROS 2 node integration, end-to-end software integration, and eventually hardware-oriented verification.

Mock-based tests are most valuable when executed automatically as part of continuous integration. Because they require no robot hardware, large suites can run whenever software changes and can execute concurrently across build agents. Failures can identify whether an interface contract, safety response, error path, or algorithm assumption has changed. This rapid feedback prevents many hardware-dependent defects from surviving until expensive laboratory or field-testing stages.

Effective mocking and stubbing ultimately depend on good software architecture. Hardware interfaces should be narrow, explicit, replaceable, and separated from algorithmic responsibilities. Tests should control inputs and failure modes without becoming tightly coupled to implementation details. When these principles are applied consistently, hardware-dependent robot software becomes easier to verify, failures become more reproducible, and later integration with real devices can focus on genuine hardware and system-level behavior.

로보틱스 소프트웨어(Robotics Software)는 일상적인 소프트웨어 테스트 과정에서 사용할 수 없거나, 비용이 많이 들거나, 동작이 느리거나, 비결정적이거나, 안전하게 운용하기 어려운 물리적 장치에 의존하는 경우가 많다. 모터(Motor), 엔코더(Encoder), 카메라(Camera), 라이다(LiDAR), 관성 측정 장치(IMU), 위성항법시스템 수신기(GNSS Receiver), 배터리 제어기(Battery Controller), 안전 장치(Safety Device) 등은 기존 단위 테스트(Unit Test)의 빠른 실행과 반복성을 방해할 수 있다. 모킹(Mocking)과 스터빙(Stubbing)은 이러한 하드웨어 의존성을 제어 가능한 소프트웨어 표현으로 대체하여 개별 구성요소를 독립적으로 검증할 수 있도록 한다.

하드웨어 추상화 경계(Hardware Abstraction Boundary)는 효과적인 모킹(Mocking)의 기반이다. 제어 또는 인지 알고리즘(Control or Perception Algorithm)이 장치 드라이버(Device Driver)와 직접 통신하도록 하는 대신, 소프트웨어는 엔코더 위치 읽기, IMU 측정값 획득, 모터 명령 전송, 장치 상태 확인 등의 동작을 정의하는 인터페이스(Interface)를 제공한다. 실제 운용 코드(Production Code)는 이 인터페이스를 실제 하드웨어에 연결하고, 단위 테스트에서는 테스트 대상 구성요소를 변경하지 않은 상태에서 모의(Mock) 또는 스텁(Stub) 구현으로 대체한다.

스텁(Stub)은 테스트 대상 소프트웨어의 요청에 대해 미리 결정된 응답을 제공한다. 예를 들어 엔코더 스텁(Encoder Stub)은 항상 알려진 휠 위치를 반환하고, IMU 스텁은 사전에 정의된 가속도 벡터를 제공하며, 배터리 스텁(Battery Stub)은 고정된 충전 상태(State of Charge)를 보고할 수 있다. 스텁은 테스트의 목적이 테스트 대상 구성요소와 의존성 사이의 세부 상호작용을 검증하는 것이 아니라 입력 조건을 제어하는 것일 때 특히 유용하다.

모의 객체(Mock)는 이러한 개념을 확장하여 상호작용을 기록하거나 검증한다. 모의 모터 인터페이스(Mock Motor Interface)는 제어기가 특정 토크 명령(Torque Command)을 전달했는지, 비상 상황에서 영속도 명령(Zero-Velocity Request)이 발생했는지, 초기화 과정에서 요구된 순서대로 장치 설정이 호출되었는지를 검증할 수 있다. 테스트는 함수 인자, 호출 횟수, 반환값, 오류 동작에 대한 기대 조건을 정의하여 계산 결과와 통신 계약(Communication Contract)을 함께 검증할 수 있다.

의존성 주입(Dependency Injection)은 이러한 대체 작업을 실용적으로 만든다. 로봇 구성요소는 내부에서 구체적인 하드웨어 드라이버를 직접 생성하는 대신 생성자(Constructor), 초기화 함수(Initialization Function), 구성 메커니즘(Configuration Mechanism)을 통해 하드웨어 인터페이스를 전달받을 수 있다. 정상 운용에서는 실제 구현이 주입되고, 테스트에서는 모의 구현(Mock Implementation)이 제공된다. 이러한 설계는 알고리즘 로직과 장치별 코드 사이의 결합도(Coupling)를 낮추면서 테스트 가능성(Testability)과 아키텍처 모듈성(Architectural Modularity)을 향상시킨다.

C++ 로보틱스 프로젝트에서는 인터페이스 지향 설계(Interface-Oriented Design)와 Google Mock과 같은 모킹 기능을 결합할 수 있다. 가상 하드웨어 인터페이스(Virtual Hardware Interface)는 readPosition(), readVelocity(), setTorque(), getStatus()와 같은 메서드를 정의하고, 모의 클래스(Mock Class)는 이에 대응하는 모의 메서드를 구현할 수 있다. 테스트에서는 제어기를 실행하기 전에 예상 호출과 반환값을 설정함으로써 실제 액추에이터(Actuator)나 센서(Sensor)를 연결하지 않고도 하드웨어 관련 동작을 검사할 수 있다.

Python 소프트웨어에서도 모의 객체(Mock Object), 몽키 패칭(Monkeypatching), 픽스처(Fixture), 경량 가짜 클래스(Fake Class)를 사용하여 유사한 격리를 구현할 수 있다. 테스트는 카메라 API를 합성 프레임(Synthetic Frame)을 반환하는 함수로 대체하거나 네트워크 연결 센서 클라이언트를 결정론적 메시지를 생성하는 객체로 대체할 수 있다. PyTest 픽스처는 이러한 대체 요소를 패키지화하여 동일한 모의 의존성을 관련 테스트 사례에서 일관되게 재사용하면서 실제 운용 리소스로부터 격리할 수 있도록 한다.

모킹(Mocking)은 특히 실패 처리(Failure Handling)를 테스트할 때 중요하다. 실제 하드웨어 장애는 의도적으로 재현하기 어렵거나 바람직하지 않은 경우가 많지만, 모의 객체는 이러한 장애를 결정론적으로 발생시킬 수 있다. 센서 인터페이스는 통신 오류를 발생시키거나, 오래된 타임스탬프를 반환하거나, 잘못된 측정값을 보고하거나, 장치 연결 해제를 모사할 수 있다. 모터 드라이버 모의 객체는 명령을 거부하거나 과열 상태(Overtemperature State)를 보고할 수 있으므로 복구 및 결함 관리 로직(Fault-Management Logic)을 안전하게 검증할 수 있다.

시간 관련 의존성(Timing-Related Dependency)도 신중하게 처리해야 한다. 로봇 소프트웨어는 시계(Clock), 타이머(Timer), 워치독(Watchdog), 타임아웃(Timeout) 메커니즘을 자주 사용하며, 실제 시간(Wall-Clock Time)에 의존하면 테스트가 불필요하게 느려질 수 있다. 모의 시계(Mock Clock)는 시간을 프로그램적으로 진행시켜 500ms 타임아웃이나 수초 길이의 워치독 상태 전이를 거의 즉시 검증할 수 있게 한다. 시간을 제어하면 간헐적이고 재현하기 어려운 테스트 실패를 발생시킬 수 있는 스케줄링 변동(Scheduling Variation)도 제거할 수 있다.

센서 스텁(Sensor Stub)은 임의의 값이 아니라 의미 있는 물리적 조건을 표현해야 한다. IMU 테스트 시퀀스(Test Sequence)는 정지된 로봇, 일정한 각운동(Constant Angular Motion), 갑작스러운 외란(Sudden Disturbance)을 표현할 수 있으며, 엔코더 값은 전진 이동 또는 휠 슬립(Wheel Slip)을 나타낼 수 있다. 인식 가능한 운용 조건을 중심으로 입력을 구성하면 개발자가 테스트 실패를 예상된 로봇 동작과 연관시킬 수 있고 알고리즘 수준의 회귀 테스트(Regression Testing)를 위한 재사용 가능한 데이터셋을 구축할 수 있다.

액추에이터 모킹(Actuator Mocking)은 실제 물리적 움직임이 발생하지 않으므로 주로 명령과 안전 제약조건(Safety Constraint)을 검증하는 데 초점을 둔다. 테스트에서는 속도, 전류, 토크, 조향각(Steering Angle), 관절 위치(Joint Position) 명령이 설정된 제한 범위 내에 유지되는지 확인할 수 있다. 또한 잘못된 상태 추정값, 통신 장애, 안전 이벤트(Safety Event)가 정상 명령을 억제하는지도 검증할 수 있다. 이러한 접근법은 동일한 로직을 실제 액추에이터에 연결하기 전에 소프트웨어가 명령 계약(Command Contract)을 준수한다는 초기 증거를 제공한다.

모의 객체(Mock)는 실제 장치의 모든 내부 세부사항을 재현해서는 안 된다. 지나치게 상세한 모의 객체는 하드웨어 드라이버의 또 다른 구현체가 될 수 있으며, 실제 드라이버의 결함이나 가정을 그대로 복제할 가능성이 있다. 더 나은 설계는 테스트 대상 소프트웨어가 요구하는 외부 관측 가능 계약(Externally Observable Contract)만 모델링하는 것이다. 현실적인 장치 동역학(Device Dynamics)이나 프로토콜 동작이 필요해지면 테스트는 점진적으로 시뮬레이션(Simulation), 소프트웨어 통합(Software Integration), 하드웨어 인더루프(HIL, Hardware-in-the-Loop) 환경으로 이동해야 한다.

따라서 스텁(Stub), 모의 객체(Mock), 가짜 객체(Fake), 시뮬레이터(Simulator)는 서로 다른 검증 목적을 가진다. 스텁은 제어된 데이터를 제공하고, 모의 객체는 상호작용을 검증하며, 가짜 객체는 인메모리 장치 서비스(In-Memory Device Service)와 같은 단순화되었지만 실제로 동작하는 구현을 제공할 수 있다. 시뮬레이터는 물리적 또는 시간적 동작을 더 높은 충실도(Fidelity)로 표현한다. 검증 목적을 충족하는 가장 단순한 테스트 대역(Test Double)을 선택하면 단위 테스트를 이해하기 쉽고 결정론적이며 계산 비용이 낮은 상태로 유지할 수 있다.

테스트 대역(Test Double)은 정상적인 하드웨어에서 재현하기 어려운 비정상적인 경계 조건도 표현해야 한다. 여기에는 센서 포화값(Saturated Sensor Value), 패킷 손실(Packet Loss), 지연된 응답(Delayed Response), 잘못된 체크섬(Invalid Checksum), 반복되는 타임스탬프, 엔코더 롤오버(Encoder Rollover), 간헐적 연결(Intermittent Connectivity), 초기화 실패(Initialization Failure) 등이 포함된다. 이러한 조건을 체계적으로 주입하면 로봇 소프트웨어가 손상된 데이터를 전파하거나 제어되지 않은 명령을 발생시키는 대신 정의된 성능 저하 상태(Degraded State) 또는 안전 상태(Safe State)로 전환되는지 확인할 수 있다.

모킹(Mocking)과 통합 테스트(Integration Testing)의 경계는 명확하게 유지해야 한다. 모의 모터 드라이버를 이용한 제어기 테스트는 제어기가 드라이버 인터페이스를 올바르게 사용한다는 것을 입증하지만, 실제 운용 드라이버가 물리적 모터와 정확하게 통신한다는 것을 입증하지는 않는다. 이러한 증거는 더 높은 테스트 수준에서 확보해야 한다. 따라서 테스트 구조는 격리된 소프트웨어 의존성 검증에서 ROS 2 노드 통합, 종단 간 소프트웨어 통합(End-to-End Software Integration), 최종적으로 하드웨어 중심 검증(Hardware-Oriented Verification)으로 점진적으로 확장된다.

모의 객체 기반 테스트(Mock-Based Test)는 지속적 통합(CI, Continuous Integration)의 일부로 자동 실행될 때 가장 큰 가치를 가진다. 로봇 하드웨어가 필요하지 않기 때문에 대규모 테스트 스위트를 소프트웨어가 변경될 때마다 실행할 수 있으며 여러 빌드 에이전트(Build Agent)에서 동시에 수행할 수도 있다. 테스트 실패를 통해 인터페이스 계약, 안전 대응, 오류 처리 경로(Error Path), 알고리즘 가정(Algorithm Assumption)의 변경 여부를 식별할 수 있다. 이러한 빠른 피드백은 많은 하드웨어 의존 결함이 비용이 높은 실험실 또는 현장 테스트 단계까지 남아 있는 것을 방지한다.

효과적인 모킹(Mocking)과 스터빙(Stubbing)은 궁극적으로 우수한 소프트웨어 아키텍처(Software Architecture)에 의존한다. 하드웨어 인터페이스는 범위가 명확하고, 명시적이며, 교체 가능해야 하고, 알고리즘의 책임과 분리되어야 한다. 테스트는 구현 세부사항에 지나치게 결합되지 않으면서 입력과 실패 모드(Failure Mode)를 제어할 수 있어야 한다. 이러한 원칙을 일관되게 적용하면 하드웨어 의존 로봇 소프트웨어의 검증이 쉬워지고, 장애 재현성이 향상되며, 이후 실제 장치와의 통합 과정에서는 진정한 하드웨어 및 시스템 수준 동작에 집중할 수 있다.

##  

## 02.03. ROS2 Unit Test ament cmake gtest [w/Code]

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

ROS 2 software combines ordinary C++ logic with middleware-specific concepts such as nodes, publishers, subscribers, services, parameters, executors, and lifecycle behavior. Unit testing should therefore verify algorithmic and component behavior before larger node graphs are assembled. Within the software unit and integration testing structure, ament_cmake_gtest provides a standard way to connect GoogleTest-based C++ tests with ROS 2 package builds and automated test execution.

The ROS 2 build environment is based on ament and commonly uses ament_cmake for C++ packages. Tests are normally declared in the package CMake configuration so they become part of the same dependency and build model as production code. Instead of compiling a standalone test manually, developers register the test target through ament_cmake_gtest, associate the required libraries and ROS 2 dependencies, and allow the build system to manage execution and result collection.

A typical ROS 2 unit test separates reusable logic from the executable node that hosts it. Algorithms for coordinate conversion, command limiting, state validation, filtering, trajectory processing, or message interpretation can be implemented in ordinary C++ classes or libraries. GoogleTest can then instantiate those objects directly without launching an entire ROS graph, making failures easier to localize and keeping execution significantly faster than system-level tests.

The CMakeLists.txt file acts as the integration point between GoogleTest and the ROS 2 package. Testing configuration is generally placed behind the BUILD_TESTING condition so production builds do not unnecessarily configure test targets. The package locates ament_cmake_gtest as a test dependency and registers a source file as a GoogleTest executable. Additional target dependencies are then attached according to the interfaces exercised by the unit under test.

Package metadata should describe testing dependencies separately from normal runtime requirements where appropriate. Declaring the testing framework in package.xml allows dependency management tools and CI environments to reproduce the required build environment. This is important for robotics projects because tests may execute on developer workstations, container images, dedicated build servers, or multiple target architectures, and each environment must resolve the same package-level testing requirements.

GoogleTest assertions provide the fundamental verification mechanism inside ROS 2 C++ unit tests. EXPECT_EQ can verify discrete states or identifiers, EXPECT_TRUE can validate logical conditions, and EXPECT_NEAR is appropriate for numerical calculations involving floating-point tolerances. ASSERT-style checks terminate the current test when a prerequisite fails, preventing later expressions from operating on invalid objects or meaningless intermediate results.

Test fixtures are useful when ROS 2-related initialization is shared across several test cases. A fixture can construct a component, prepare messages, initialize parameters, or create deterministic test inputs before each test. Common cleanup can also be centralized. When ROS client-library initialization is actually required, its lifecycle should be controlled explicitly so repeated tests do not inherit hidden middleware state from previous cases.

Parameter handling is an important target for ROS 2 unit tests because many robot behaviors are configured at deployment time. Tests can verify default values, valid overrides, range checks, missing configuration, and rejection of invalid combinations. A velocity controller, for example, should behave predictably when maximum speed or acceleration parameters are changed and should not silently accept values that violate the component\'s defined operating constraints.

ROS 2 message-processing functions should also be tested independently whenever possible. A callback often contains validation, conversion, filtering, or state-update logic that does not fundamentally require DDS communication. Extracting this logic into testable functions allows synthetic geometry, sensor, navigation, or control messages to be passed directly into the unit, enabling deterministic verification without discovery delays, network transport, or executor scheduling effects.

Time introduces another important boundary. Robot nodes frequently evaluate message age, timeout conditions, watchdog intervals, and timestamp consistency. Tests should avoid unnecessary dependence on uncontrolled wall-clock timing because scheduling variations can create flaky results. Where architecture permits, time should be supplied through a controllable abstraction or explicit timestamp input so timeout and stale-data behavior can be verified quickly and repeatably.

Hardware access should remain outside the scope of most ROS 2 unit tests. A controller node should not require a real motor drive simply to test command saturation, and a perception component should not require a physical camera to test message validation. Hardware interfaces can instead be replaced with mocks, stubs, or synthetic data, preserving the isolation established by unit testing while leaving actual device communication for later integration and HIL verification.

The colcon workflow allows tests from multiple ROS 2 packages to be built and executed consistently across a workspace. After compilation, registered tests can be executed through the workspace testing process, and their results can be inspected in a consolidated form. This enables developers to detect failures across package boundaries while still retaining individual GoogleTest diagnostics that identify the exact test case and assertion responsible for a regression.

A useful ROS 2 unit test should remain independent of discovery timing and communication races whenever the behavior under examination does not require them. Tests that depend on publishers discovering subscribers, executors spinning for arbitrary delays, or messages arriving within loosely selected sleep intervals begin to behave like integration tests. Such behavior belongs in a later layer where ROS 2 communication semantics are deliberately part of the verification objective.

The distinction between unit and integration testing is therefore architectural rather than merely based on which framework launches the test. A GoogleTest executable that directly verifies a command-limiting class is a unit test, while a test that creates multiple ROS 2 nodes and verifies messages traveling through topics exercises integration behavior. Keeping this boundary explicit helps teams maintain fast unit suites while developing separate tests for node graph communication.

Failure-path testing is particularly valuable for robot nodes. Synthetic inputs can represent malformed messages, out-of-range commands, stale sensor data, unavailable configuration, invalid state transitions, or numerical anomalies. The expected result may be rejection, diagnostic reporting, command suppression, or transition into a defined safe state. Testing these conditions without physical hardware provides rapid evidence that defensive software behavior remains intact after code changes.

ROS 2 unit tests become most effective when integrated into continuous integration. Each change can trigger package compilation followed by registered ament tests, with failed assertions preventing defective changes from progressing further through the delivery pipeline. Because isolated tests are relatively fast and require little infrastructure, they can run much more frequently than simulation, HIL, or field tests and provide the earliest ROS-specific regression feedback.

Maintaining these tests requires the same discipline as maintaining production code. Test names should describe observable behavior, fixtures should avoid unnecessary complexity, numerical tolerances should have engineering justification, and tests should not depend excessively on private implementation details. When an internal refactoring preserves the external contract of a component, well-designed tests should normally continue to pass rather than requiring extensive modification.

ament_cmake_gtest therefore connects conventional C++ unit-testing practice with the ROS 2 package and build ecosystem. Its primary value is not simply launching GoogleTest, but making component-level verification reproducible within the same workspace used to build robot software. Combined with clean interfaces, controlled dependencies, deterministic inputs, and CI execution, it establishes a fast verification layer before ROS 2 node integration, end-to-end software testing, simulation, and hardware validation.

ROS 2 소프트웨어는 일반적인 C++ 로직과 함께 노드(Node), 퍼블리셔(Publisher), 서브스크라이버(Subscriber), 서비스(Service), 매개변수(Parameter), 실행기(Executor), 수명주기 동작(Lifecycle Behavior)과 같은 미들웨어(Middleware) 고유 개념을 결합한다. 따라서 단위 테스트(Unit Testing)는 더 큰 노드 그래프(Node Graph)를 구성하기 전에 알고리즘과 구성요소의 동작을 검증해야 한다. 소프트웨어 단위 및 통합 테스트(Software Unit and Integration Testing) 구조에서 ament_cmake_gtest는 GoogleTest 기반 C++ 테스트를 ROS 2 패키지 빌드 및 자동화된 테스트 실행과 연결하는 표준적인 방법을 제공한다.

ROS 2 빌드 환경(Build Environment)은 ament를 기반으로 하며 C++ 패키지에서는 일반적으로 ament_cmake를 사용한다. 테스트는 일반적으로 패키지의 CMake 구성에 선언되어 실제 운용 코드(Production Code)와 동일한 의존성 및 빌드 모델의 일부가 된다. 개발자가 독립형 테스트를 수동으로 컴파일하는 대신 ament_cmake_gtest를 통해 테스트 대상(Test Target)을 등록하고 필요한 라이브러리와 ROS 2 의존성을 연결하면 빌드 시스템이 실행 및 결과 수집을 관리할 수 있다.

일반적인 ROS 2 단위 테스트는 재사용 가능한 로직을 해당 로직을 실행하는 노드(Node)와 분리한다. 좌표 변환(Coordinate Conversion), 명령 제한(Command Limiting), 상태 검증(State Validation), 필터링(Filtering), 궤적 처리(Trajectory Processing), 메시지 해석(Message Interpretation)을 위한 알고리즘은 일반적인 C++ 클래스 또는 라이브러리로 구현할 수 있다. 이후 GoogleTest에서 전체 ROS 그래프를 실행하지 않고 해당 객체를 직접 생성할 수 있으므로 실패 원인을 쉽게 국소화하고 시스템 수준 테스트보다 훨씬 빠르게 실행할 수 있다.

CMakeLists.txt 파일은 GoogleTest와 ROS 2 패키지를 연결하는 통합 지점(Integration Point)의 역할을 한다. 테스트 구성은 일반적으로 BUILD_TESTING 조건 내부에 배치하여 실제 운용 빌드에서 불필요하게 테스트 대상을 구성하지 않도록 한다. 패키지는 ament_cmake_gtest를 테스트 의존성(Test Dependency)으로 탐색하고 소스 파일을 GoogleTest 실행 파일로 등록한다. 이후 테스트 대상 단위(Unit Under Test)가 사용하는 인터페이스에 따라 추가적인 대상 의존성을 연결한다.

패키지 메타데이터(Package Metadata)는 필요한 경우 테스트 의존성을 일반적인 런타임 요구사항(Runtime Requirement)과 별도로 기술해야 한다. package.xml에 테스트 프레임워크(Testing Framework)를 선언하면 의존성 관리 도구와 지속적 통합(CI, Continuous Integration) 환경에서 필요한 빌드 환경을 재현할 수 있다. 로보틱스 프로젝트의 테스트는 개발자 워크스테이션, 컨테이너 이미지(Container Image), 전용 빌드 서버 또는 다양한 대상 아키텍처에서 실행될 수 있으므로 각 환경에서 동일한 패키지 수준 테스트 요구사항을 해결할 수 있어야 한다.

GoogleTest 어설션(Assertion)은 ROS 2 C++ 단위 테스트 내부에서 기본적인 검증 메커니즘을 제공한다. EXPECT_EQ는 이산 상태나 식별자를 검증할 수 있고, EXPECT_TRUE는 논리 조건을 확인할 수 있으며, EXPECT_NEAR는 부동소수점 허용오차(Floating-Point Tolerance)가 포함된 수치 계산에 적합하다. ASSERT 계열 검사는 필수 선행 조건이 실패하면 현재 테스트를 종료하여 이후 표현식이 유효하지 않은 객체나 의미 없는 중간 결과를 대상으로 동작하는 것을 방지한다.

테스트 픽스처(Test Fixture)는 여러 테스트 사례(Test Case)가 ROS 2 관련 초기화 작업을 공유할 때 유용하다. 픽스처는 각 테스트 전에 구성요소를 생성하고, 메시지를 준비하며, 매개변수를 초기화하거나 결정론적 테스트 입력(Deterministic Test Input)을 생성할 수 있다. 공통 정리 작업(Cleanup)도 중앙에서 관리할 수 있다. ROS 클라이언트 라이브러리 초기화가 실제로 필요한 경우에는 수명주기(Lifecycle)를 명시적으로 제어하여 반복되는 테스트가 이전 테스트에서 남은 숨겨진 미들웨어 상태를 상속하지 않도록 해야 한다.

매개변수 처리(Parameter Handling)는 많은 로봇 동작이 배포 시점에 구성되므로 ROS 2 단위 테스트의 중요한 검증 대상이다. 테스트에서는 기본값(Default Value), 유효한 재정의(Valid Override), 범위 검사(Range Check), 누락된 구성(Missing Configuration), 잘못된 조합의 거부 등을 검증할 수 있다. 예를 들어 속도 제어기(Velocity Controller)는 최대 속도 또는 가속도 매개변수가 변경되었을 때 예측 가능한 방식으로 동작해야 하며, 구성요소에 정의된 운용 제약조건을 위반하는 값을 아무런 검증 없이 허용해서는 안 된다.

ROS 2 메시지 처리 함수(Message-Processing Function)도 가능한 경우 독립적으로 테스트해야 한다. 콜백(Callback)은 DDS 통신 자체를 반드시 필요로 하지 않는 검증, 변환, 필터링 또는 상태 갱신 로직을 포함하는 경우가 많다. 이러한 로직을 테스트 가능한 함수로 분리하면 합성된 기하학, 센서, 내비게이션 또는 제어 메시지를 테스트 대상 단위에 직접 전달할 수 있으므로 디스커버리 지연(Discovery Delay), 네트워크 전송(Network Transport), 실행기 스케줄링(Executor Scheduling)의 영향 없이 결정론적인 검증이 가능하다.

시간(Time)은 또 다른 중요한 경계 요소이다. 로봇 노드는 메시지의 경과 시간, 타임아웃(Timeout) 조건, 워치독 간격(Watchdog Interval), 타임스탬프 일관성(Timestamp Consistency)을 자주 평가한다. 스케줄링 변동으로 인해 불안정한 테스트(Flaky Test)가 발생할 수 있으므로 테스트는 제어되지 않는 실제 시간(Wall-Clock Timing)에 불필요하게 의존하지 않아야 한다. 아키텍처가 허용하는 경우 제어 가능한 추상화 또는 명시적인 타임스탬프 입력을 통해 시간을 제공하여 타임아웃과 오래된 데이터(Stale Data) 동작을 빠르고 반복 가능하게 검증해야 한다.

대부분의 ROS 2 단위 테스트에서는 하드웨어 접근(Hardware Access)을 범위 밖에 두어야 한다. 제어기 노드가 명령 포화(Command Saturation)를 테스트하기 위해 실제 모터 드라이브를 필요로 해서는 안 되며, 인지 구성요소(Perception Component)가 메시지 검증을 위해 실제 카메라를 요구해서도 안 된다. 대신 하드웨어 인터페이스를 모의 객체(Mock), 스텁(Stub), 합성 데이터(Synthetic Data)로 대체하여 단위 테스트의 격리성을 유지하고 실제 장치 통신은 이후 통합 테스트 및 하드웨어 인더루프(HIL, Hardware-in-the-Loop) 검증 단계에서 수행해야 한다.

colcon 작업 흐름(Workflow)을 사용하면 여러 ROS 2 패키지의 테스트를 하나의 작업공간(Workspace)에서 일관되게 빌드하고 실행할 수 있다. 컴파일 이후 등록된 테스트를 작업공간 테스트 절차를 통해 실행하고 그 결과를 통합된 형태로 확인할 수 있다. 이를 통해 개발자는 패키지 경계를 넘어 발생하는 실패를 탐지하면서도 회귀(Regression)의 원인이 된 정확한 테스트 사례와 어설션을 식별하는 개별 GoogleTest 진단 정보를 유지할 수 있다.

유용한 ROS 2 단위 테스트는 검증하려는 동작에 해당 기능이 필요하지 않은 경우 디스커버리 타이밍(Discovery Timing)과 통신 경쟁 상태(Communication Race)에 독립적이어야 한다. 퍼블리셔가 서브스크라이버를 발견할 때까지 기다리거나, 실행기를 임의의 시간 동안 스핀(Spin)하거나, 느슨하게 설정된 대기 시간 내에 메시지가 도착하기를 기대하는 테스트는 점차 통합 테스트(Integration Test)의 특성을 갖게 된다. 이러한 동작은 ROS 2 통신 의미론(Communication Semantics) 자체가 의도적인 검증 대상이 되는 이후 테스트 계층에서 다루는 것이 적절하다.

따라서 단위 테스트와 통합 테스트의 구분은 단순히 어떤 프레임워크가 테스트를 실행하는지에 따라 결정되는 것이 아니라 아키텍처적 범위(Architectural Scope)에 따라 결정된다. 명령 제한 클래스(Command-Limiting Class)를 직접 검증하는 GoogleTest 실행 파일은 단위 테스트이지만, 여러 ROS 2 노드를 생성하고 토픽(Topic)을 통해 전달되는 메시지를 검증하는 테스트는 통합 동작을 검사한다. 이러한 경계를 명확하게 유지하면 팀은 빠른 단위 테스트 스위트(Unit Test Suite)를 유지하면서 노드 그래프 통신을 위한 별도의 테스트를 개발할 수 있다.

실패 경로 테스트(Failure-Path Testing)는 로봇 노드에서 특히 중요하다. 합성 입력을 이용하여 잘못 구성된 메시지(Malformed Message), 범위를 벗어난 명령, 오래된 센서 데이터, 사용할 수 없는 구성, 잘못된 상태 전이(Invalid State Transition), 수치적 이상(Numerical Anomaly)을 표현할 수 있다. 예상 결과는 입력 거부, 진단 보고(Diagnostic Reporting), 명령 억제(Command Suppression), 정의된 안전 상태(Safe State)로의 전환 등이 될 수 있다. 물리적 하드웨어 없이 이러한 조건을 테스트하면 코드 변경 이후에도 방어적 소프트웨어 동작(Defensive Software Behavior)이 유지되는지를 신속하게 확인할 수 있다.

ROS 2 단위 테스트는 지속적 통합(CI)에 포함될 때 가장 효과적이다. 각각의 변경사항은 패키지 컴파일과 등록된 ament 테스트 실행을 유발할 수 있으며, 실패한 어설션은 결함이 있는 변경사항이 전달 파이프라인(Delivery Pipeline)의 다음 단계로 진행되는 것을 방지한다. 격리된 테스트는 비교적 빠르고 필요한 인프라가 적기 때문에 시뮬레이션(Simulation), HIL 또는 현장 테스트(Field Test)보다 훨씬 자주 실행할 수 있으며 ROS 관련 회귀에 대한 가장 빠른 피드백을 제공한다.

이러한 테스트를 유지하려면 실제 운용 코드와 동일한 수준의 규율이 필요하다. 테스트 이름은 관측 가능한 동작(Observable Behavior)을 설명해야 하고, 픽스처는 불필요한 복잡성을 피해야 하며, 수치 허용오차(Numerical Tolerance)는 공학적 근거를 가져야 한다. 또한 테스트는 비공개 구현 세부사항(Private Implementation Detail)에 과도하게 의존해서는 안 된다. 내부 리팩터링(Refactoring)이 구성요소의 외부 계약(External Contract)을 유지한다면 잘 설계된 테스트는 대규모 수정 없이도 정상적으로 통과해야 한다.

ament_cmake_gtest는 기존 C++ 단위 테스트 실무를 ROS 2 패키지 및 빌드 생태계(Build Ecosystem)와 연결한다. 핵심 가치는 단순히 GoogleTest를 실행하는 데 있는 것이 아니라 로봇 소프트웨어를 빌드하는 동일한 작업공간 안에서 구성요소 수준 검증(Component-Level Verification)을 재현 가능하게 만드는 데 있다. 명확한 인터페이스, 제어된 의존성, 결정론적 입력, 지속적 통합 실행과 결합하면 ROS 2 노드 통합, 종단 간 소프트웨어 테스트(End-to-End Software Testing), 시뮬레이션 및 하드웨어 검증 이전에 빠르고 안정적인 검증 계층을 구축할 수 있다.

##  

## 02.04. Controller Algorithm Unit Test PID WBC [w/Code]

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

Controller algorithms transform desired robot behavior into commands that ultimately drive physical actuators, making software defects capable of producing instability, saturation, excessive force, or unsafe motion. Unit testing provides an early verification layer in which controller mathematics and software logic are examined without motors, sensors, middleware timing, or complete robot hardware. PID and whole-body control algorithms represent two important examples of this controller-level verification.

A controller unit test should isolate the computational function that maps state, reference, parameters, and time information into a control output. Instead of running a complete robot node, the test supplies deterministic position, velocity, force, or pose values directly to the controller. The resulting command is then compared with an analytically calculated value, a trusted reference implementation, or explicitly defined behavioral constraints.

PID controller testing begins with the proportional term because its expected behavior is straightforward. For a known reference and measured state, the error can be calculated directly and multiplied by the proportional gain. Tests should verify positive and negative errors, zero error, gain changes, and command direction. Such cases can reveal sign mistakes, incorrect error definitions, unit conversion defects, or accidental use of an incorrect gain parameter.

The integral term requires tests that explicitly control elapsed time and accumulated error. A sequence of constant errors should produce predictable integral growth according to the configured sampling interval. Tests should also verify reset behavior, integral limits, and anti-windup mechanisms. When an actuator command reaches saturation, the integral state must behave according to the controller design rather than continuing uncontrolled accumulation that could delay recovery.

Derivative behavior should be tested using controlled changes in error or measurement. A constant error should normally produce no derivative contribution after initialization, while a known rate of change should generate a predictable response. Tests must account for whether differentiation is performed on error or measurement and whether filtering is applied. Initialization deserves special attention because an undefined previous sample can otherwise generate an artificial derivative spike.

Sampling time is a critical input for discrete controllers. Unit tests should evaluate nominal update intervals as well as zero, unusually small, large, or inconsistent time steps according to the controller\'s defined contract. A controller should not silently divide by an invalid interval or produce unbounded output. Explicit control of time also prevents test results from depending on workstation scheduling or nondeterministic wall-clock execution.

Output saturation tests verify that controller commands remain within actuator or system limits. Large tracking errors can be intentionally supplied so the unconstrained PID result exceeds the configured maximum or minimum command. The test then confirms that the final output is clamped correctly. Related tests should verify asymmetric limits, disabled limits, configuration changes, and recovery from saturation without violating the intended internal controller state.

Controller state initialization and reset behavior are equally important. A newly constructed controller should begin from a documented internal state, and reset operations should clear or preserve integral, derivative, filter, and previous-sample values exactly as specified. These tests are particularly useful after mode transitions, emergency stops, controller switching, or trajectory restarts where stale internal state could generate an unexpected command.

Numerical robustness should be verified around boundary conditions. Tests can provide extremely small errors, values close to configured limits, large but valid state values, and floating-point conditions relevant to the implementation. Comparisons should use engineering tolerances rather than exact equality where appropriate. Invalid NaN or infinite inputs should be handled according to an explicit software policy instead of being allowed to propagate unpredictably into actuator commands.

Whole-body control(WBC) requires a broader unit-testing strategy because its output may depend on robot dynamics, task objectives, contact constraints, joint limits, and optimization variables. The test should decompose the implementation into independently verifiable mathematical components wherever possible. Kinematic mappings, Jacobians, task errors, dynamic terms, constraint construction, and optimization outputs can then be examined before testing the complete WBC computation.

Kinematic quantities provide useful deterministic test targets. For a predefined robot configuration, a unit test can compare calculated forward kinematics, Jacobians, or task-space errors with trusted reference values. Special configurations should be included where relevant because singular or nearly singular Jacobians can expose numerical weaknesses. Small perturbations of joint states can also verify whether calculated task-space changes remain consistent with expected local kinematic behavior.

Dynamic computations can be tested using fixed joint position and velocity vectors together with known robot-model parameters. Mass matrices should satisfy expected dimensional and structural properties, while gravity and bias terms can be compared against reference calculations. Unit tests should verify coordinate ordering and matrix dimensions carefully because indexing mistakes may produce numerically valid outputs that nevertheless correspond to the wrong joints or degrees of freedom.

Contact handling is central to many WBC implementations for humanoids, quadrupeds, and mobile manipulators. Tests can construct predefined contact states and verify that the appropriate constraints are activated or removed. Contact forces, friction constraints, support conditions, and allowable motion directions should be checked against the controller formulation. Switching a foot or end effector between contact and free motion should result in predictable changes to the optimization problem.

Task prioritization must also be verified when WBC combines several objectives. A test can introduce conflicting posture, end-effector, balance, or center-of-mass objectives and examine whether the resulting solution follows the configured hierarchy or weighting policy. Changing task weights should influence the solution in the intended direction. Such tests are valuable because configuration or matrix-assembly defects can silently reverse priorities without causing a solver failure.

Constraint tests should examine joint position, velocity, torque, acceleration, and contact-force limits where they are part of the controller formulation. Inputs can deliberately request an infeasible or near-limit motion so the test can verify whether constraints are respected. The expected behavior for an infeasible optimization problem should also be defined, including whether the controller reports failure, retains a previous command, or transitions toward a safe fallback.

Optimization-based controllers require verification beyond checking that the solver reports success. Tests should inspect solution dimensions, finite numerical values, constraint satisfaction, residuals, and relevant optimality conditions when practical. A solver can return a technically successful result while upstream matrices contain incorrect signs or coordinate mappings. Reference scenarios with simple known solutions are therefore especially valuable for detecting formulation errors.

Determinism is essential for controller regression testing. Identical state vectors, references, model parameters, and time steps should produce equivalent results within defined numerical tolerances. Randomized tests may supplement deterministic cases, but their seeds should be controlled so failures can be reproduced. Controller tests should execute without ROS 2 communication, physical actuators, or real-time scheduling unless those mechanisms are specifically part of a higher-level verification objective.

Controller unit tests provide mathematical and software evidence, not proof of physical stability on a real robot. A PID test can establish correct equations and saturation behavior, while WBC tests can establish correct matrix construction and constraint handling. Actual timing, actuator dynamics, sensor noise, communication delay, structural compliance, and contact uncertainty require later simulation, integration, HIL, and field validation stages within the broader testing hierarchy.

When incorporated into continuous integration, PID and WBC unit tests become regression guards for safety-critical control software. Changes to gains, robot models, optimization libraries, numerical routines, or controller architecture can automatically trigger deterministic verification before deployment. This preserves a fast feedback layer between low-level software changes and more expensive physical testing, while providing traceable evidence that fundamental controller behavior remains consistent as the robot platform evolves.

제어기 알고리즘(Controller Algorithm)은 원하는 로봇 동작을 최종적으로 물리적 액추에이터(Actuator)를 구동하는 명령으로 변환하므로 소프트웨어 결함이 불안정성, 포화(Saturation), 과도한 힘 또는 위험한 움직임을 발생시킬 수 있다. 단위 테스트(Unit Testing)는 모터, 센서, 미들웨어 타이밍(Middleware Timing), 완전한 로봇 하드웨어 없이 제어기의 수학적 계산과 소프트웨어 로직을 검사하는 초기 검증 계층을 제공한다. PID와 전신 제어(WBC, Whole-Body Control) 알고리즘은 이러한 제어기 수준 검증의 대표적인 사례이다.

제어기 단위 테스트(Controller Unit Test)는 상태(State), 기준값(Reference), 매개변수(Parameter), 시간 정보를 제어 출력(Control Output)으로 변환하는 계산 함수를 격리해야 한다. 전체 로봇 노드를 실행하는 대신 테스트에서 결정론적인 위치, 속도, 힘 또는 자세(Pose) 값을 제어기에 직접 제공한다. 이후 생성된 명령을 해석적으로 계산한 값, 신뢰할 수 있는 참조 구현(Reference Implementation), 또는 명시적으로 정의된 동작 제약조건(Behavioral Constraint)과 비교한다.

PID 제어기 테스트는 예상 동작이 명확한 비례항(Proportional Term)부터 시작한다. 알려진 기준값과 측정 상태에 대해 오차를 직접 계산하고 비례 이득(Proportional Gain)을 곱할 수 있다. 테스트에서는 양의 오차와 음의 오차, 영 오차(Zero Error), 이득 변경, 명령 방향을 검증해야 한다. 이러한 테스트를 통해 부호 오류, 잘못된 오차 정의, 단위 변환 결함 또는 잘못된 이득 매개변수를 사용하는 문제를 발견할 수 있다.

적분항(Integral Term)은 경과 시간과 누적 오차(Accumulated Error)를 명시적으로 제어하는 테스트가 필요하다. 일정한 오차가 연속적으로 입력되면 설정된 샘플링 간격(Sampling Interval)에 따라 예측 가능한 적분 증가가 발생해야 한다. 테스트에서는 초기화 동작, 적분 제한(Integral Limit), 안티 와인드업(Anti-Windup) 메커니즘도 검증해야 한다. 액추에이터 명령이 포화 상태에 도달하면 적분 상태가 계속 무제한으로 누적되어 복구를 지연시키는 대신 제어기 설계에 정의된 방식으로 동작해야 한다.

미분 동작(Derivative Behavior)은 제어된 오차 또는 측정값의 변화를 이용하여 테스트해야 한다. 일정한 오차는 일반적으로 초기화 이후 미분 성분을 발생시키지 않아야 하며, 알려진 변화율은 예측 가능한 응답을 생성해야 한다. 테스트에서는 미분이 오차(Error)를 기준으로 수행되는지 측정값(Measurement)을 기준으로 수행되는지, 그리고 필터링(Filtering)이 적용되는지를 고려해야 한다. 정의되지 않은 이전 샘플이 인위적인 미분 스파이크(Derivative Spike)를 발생시킬 수 있으므로 초기화 과정도 특별히 검증해야 한다.

샘플링 시간(Sampling Time)은 이산 제어기(Discrete Controller)의 중요한 입력이다. 단위 테스트에서는 정상적인 갱신 주기뿐만 아니라 제어기에 정의된 계약에 따라 0, 비정상적으로 작은 값, 큰 값 또는 일관되지 않은 시간 간격도 평가해야 한다. 제어기는 잘못된 시간 간격으로 나누기 연산을 수행하거나 무한정 증가하는 출력을 생성해서는 안 된다. 시간을 명시적으로 제어하면 테스트 결과가 워크스테이션 스케줄링이나 비결정적인 실제 시간 실행에 의존하는 것도 방지할 수 있다.

출력 포화 테스트(Output Saturation Test)는 제어기 명령이 액추에이터 또는 시스템 제한 범위 내에 유지되는지를 검증한다. 추종 오차(Tracking Error)를 의도적으로 크게 설정하여 제한되지 않은 PID 결과가 설정된 최대 또는 최소 명령을 초과하도록 만들 수 있다. 이후 최종 출력이 정확하게 제한되는지 확인한다. 관련 테스트에서는 비대칭 제한(Asymmetric Limit), 제한 기능 비활성화, 구성 변경 및 포화 상태에서 복구되는 과정에서도 의도된 내부 제어기 상태가 유지되는지를 검증해야 한다.

제어기 상태 초기화(Controller State Initialization)와 리셋 동작(Reset Behavior)도 중요하다. 새롭게 생성된 제어기는 문서화된 내부 상태에서 시작해야 하며, 리셋 동작은 정의된 사양에 따라 적분값, 미분값, 필터 상태, 이전 샘플 값을 정확하게 초기화하거나 보존해야 한다. 이러한 테스트는 모드 전환(Mode Transition), 비상 정지(Emergency Stop), 제어기 전환(Controller Switching), 궤적 재시작(Trajectory Restart) 이후 남아 있는 이전 내부 상태가 예상하지 못한 명령을 발생시키는 문제를 방지하는 데 특히 유용하다.

수치적 강건성(Numerical Robustness)은 경계 조건 주변에서 검증해야 한다. 테스트에서는 매우 작은 오차, 설정된 제한에 가까운 값, 크지만 유효한 상태값, 구현과 관련된 부동소수점 조건을 제공할 수 있다. 필요한 경우 비교에는 정확한 동일성보다 공학적으로 정의된 허용오차(Engineering Tolerance)를 사용해야 한다. 잘못된 NaN 또는 무한대(Infinite) 입력도 액추에이터 명령으로 예측 불가능하게 전파되지 않고 명시적인 소프트웨어 정책에 따라 처리되어야 한다.

전신 제어(WBC, Whole-Body Control)는 출력이 로봇 동역학(Robot Dynamics), 작업 목표(Task Objective), 접촉 제약조건(Contact Constraint), 관절 제한(Joint Limit), 최적화 변수(Optimization Variable)에 의존할 수 있으므로 더욱 광범위한 단위 테스트 전략이 필요하다. 가능한 경우 구현을 독립적으로 검증할 수 있는 수학적 구성요소로 분해해야 한다. 이후 운동학 매핑(Kinematic Mapping), 자코비안(Jacobian), 작업 오차(Task Error), 동역학 항(Dynamic Term), 제약조건 구성, 최적화 출력을 전체 WBC 계산 이전에 개별적으로 검사할 수 있다.

운동학적 수량(Kinematic Quantity)은 결정론적인 테스트 대상을 제공한다. 미리 정의된 로봇 구성(Configuration)에 대해 계산된 순기구학(Forward Kinematics), 자코비안 또는 작업 공간 오차(Task-Space Error)를 신뢰할 수 있는 기준값과 비교할 수 있다. 특이점(Singularity) 또는 특이점에 가까운 자코비안은 수치적 취약성을 드러낼 수 있으므로 관련된 특수 구성도 포함해야 한다. 관절 상태에 작은 섭동(Perturbation)을 적용하여 계산된 작업 공간 변화가 예상되는 국소 운동학 동작과 일치하는지도 검증할 수 있다.

동역학 계산(Dynamic Computation)은 고정된 관절 위치 및 속도 벡터와 알려진 로봇 모델 매개변수를 사용하여 테스트할 수 있다. 질량 행렬(Mass Matrix)은 예상되는 차원과 구조적 특성을 만족해야 하며, 중력항(Gravity Term)과 바이어스 항(Bias Term)은 기준 계산 결과와 비교할 수 있다. 인덱싱 오류는 수치적으로 유효한 결과를 생성하면서도 잘못된 관절이나 자유도(Degree of Freedom)에 대응할 수 있으므로 단위 테스트에서는 좌표 순서와 행렬 차원을 세심하게 검증해야 한다.

접촉 처리(Contact Handling)는 휴머노이드(Humanoid), 사족보행 로봇(Quadruped), 모바일 매니퓰레이터(Mobile Manipulator)를 위한 많은 WBC 구현에서 핵심적인 요소이다. 테스트에서는 미리 정의된 접촉 상태를 구성하고 적절한 제약조건이 활성화되거나 제거되는지 확인할 수 있다. 접촉력(Contact Force), 마찰 제약조건(Friction Constraint), 지지 조건(Support Condition), 허용 가능한 운동 방향을 제어기 공식과 비교해야 한다. 발 또는 말단장치(End Effector)를 접촉 상태와 자유 운동 상태 사이에서 전환하면 최적화 문제도 예측 가능한 방식으로 변경되어야 한다.

WBC가 여러 목표를 결합하는 경우 작업 우선순위(Task Prioritization)도 검증해야 한다. 테스트에서 자세(Posture), 말단장치, 균형(Balance), 질량중심(CoM, Center of Mass) 목표를 서로 충돌하도록 설정하고 결과가 구성된 계층 구조(Hierarchy) 또는 가중치 정책(Weighting Policy)을 따르는지 검사할 수 있다. 작업 가중치를 변경하면 의도된 방향으로 해가 변화해야 한다. 이러한 테스트는 구성 또는 행렬 조립(Matrix Assembly) 결함이 솔버(Solver) 실패를 발생시키지 않으면서도 우선순위를 잘못 뒤집는 문제를 탐지하는 데 유용하다.

제약조건 테스트(Constraint Test)는 제어기 공식에 포함되는 관절 위치, 속도, 토크, 가속도 및 접촉력 제한을 검사해야 한다. 의도적으로 실행 불가능하거나 제한에 가까운 동작을 요구하는 입력을 제공하여 제약조건이 준수되는지 검증할 수 있다. 실행 불가능한 최적화 문제(Infeasible Optimization Problem)가 발생했을 때의 예상 동작도 정의해야 하며, 여기에는 제어기의 실패 보고, 이전 명령 유지 또는 안전한 대체 동작(Safe Fallback)으로의 전환 등이 포함될 수 있다.

최적화 기반 제어기(Optimization-Based Controller)는 단순히 솔버가 성공을 보고했는지만 확인해서는 충분하지 않다. 테스트에서는 해의 차원, 유한한 수치값(Finite Numerical Value), 제약조건 만족 여부, 잔차(Residual), 가능한 경우 관련 최적성 조건(Optimality Condition)을 검사해야 한다. 상위 단계에서 생성된 행렬에 잘못된 부호나 좌표 매핑 오류가 있어도 솔버가 기술적으로 성공한 결과를 반환할 수 있다. 따라서 단순하면서도 알려진 해를 가진 기준 시나리오(Reference Scenario)는 공식화 오류를 탐지하는 데 특히 중요하다.

결정성(Determinism)은 제어기 회귀 테스트(Controller Regression Testing)의 핵심 요소이다. 동일한 상태 벡터, 기준값, 모델 매개변수 및 시간 간격은 정의된 수치 허용오차 내에서 동등한 결과를 생성해야 한다. 무작위 테스트(Randomized Test)를 결정론적 사례에 추가할 수 있지만 실패를 재현할 수 있도록 난수 시드(Random Seed)를 제어해야 한다. ROS 2 통신, 물리적 액추에이터 또는 실시간 스케줄링이 상위 수준 검증의 명시적인 대상이 아니라면 제어기 테스트는 이러한 요소 없이 실행되어야 한다.

제어기 단위 테스트는 수학적 및 소프트웨어적 증거를 제공하지만 실제 로봇에서의 물리적 안정성을 입증하는 것은 아니다. PID 테스트는 방정식의 정확성과 포화 동작을 검증할 수 있으며, WBC 테스트는 올바른 행렬 구성과 제약조건 처리를 검증할 수 있다. 실제 타이밍, 액추에이터 동역학, 센서 노이즈(Sensor Noise), 통신 지연(Communication Delay), 구조적 순응성(Structural Compliance), 접촉 불확실성(Contact Uncertainty)은 이후 시뮬레이션, 통합 테스트, 하드웨어 인더루프(HIL), 현장 검증(Field Validation) 단계에서 검증해야 한다.

PID 및 WBC 단위 테스트를 지속적 통합(CI, Continuous Integration)에 포함하면 안전 중요 제어 소프트웨어(Safety-Critical Control Software)를 위한 회귀 방어 장치(Regression Guard)로 활용할 수 있다. 이득, 로봇 모델, 최적화 라이브러리, 수치 계산 루틴 또는 제어기 아키텍처가 변경되면 배포 전에 결정론적인 검증을 자동으로 실행할 수 있다. 이를 통해 저수준 소프트웨어 변경과 비용이 높은 물리적 테스트 사이에 빠른 피드백 계층을 유지하면서 로봇 플랫폼이 발전하는 과정에서도 기본적인 제어기 동작이 일관되게 유지된다는 추적 가능한 증거를 확보할 수 있다.

##  

## 02.05. Perception Model Inference Unit Test [w/Code]

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

Perception model inference is a critical software boundary between raw sensor observations and the higher-level decisions made by a robot. Unit testing at this boundary verifies that model loading, input preparation, inference execution, output interpretation, and failure handling behave consistently before the perception component is evaluated as part of a complete ROS 2 graph or physical robot. This testing layer belongs within the broader software unit and integration testing structure.

An inference unit test should isolate the smallest practical execution path around the deployed model. The test can provide a deterministic image, point cloud tensor, depth map, feature vector, or other predefined input directly to the inference interface and inspect the resulting outputs. Camera drivers, ROS 2 transport, network services, and physical sensors should normally remain outside this test boundary so failures can be attributed specifically to inference software.

Model initialization is one of the first behaviors that should be verified. Tests should confirm that a valid model artifact can be loaded, required input and output bindings are available, expected tensor dimensions are recognized, and the inference object reaches a usable state. Invalid model paths, incompatible artifacts, missing metadata, unsupported tensor shapes, or initialization failures should produce explicit errors rather than undefined behavior later in execution.

Input preprocessing must be tested independently because small preprocessing differences can significantly change AI model outputs. Image resizing, cropping, normalization, channel ordering, color conversion, tensor layout, and datatype conversion should produce known results for controlled inputs. For LiDAR or depth models, tests may similarly verify coordinate normalization, range filtering, voxelization, padding, or point sampling before the data reaches the network.

Tensor shape and datatype validation provide an important defensive boundary. Tests should supply correctly shaped tensors as well as inputs with missing dimensions, unexpected batch sizes, incompatible channel counts, or unsupported numerical types. The inference wrapper should either transform supported inputs according to its contract or reject invalid data clearly. Silent reinterpretation of an incorrectly shaped tensor can produce plausible but dangerously incorrect perception results.

Deterministic reference inputs are useful for regression testing. A small set of fixed sensor samples can be passed through the same deployed model version and the outputs compared against stored reference characteristics. Exact equality may not always be appropriate because GPU kernels, optimization backends, or numerical precision can introduce small variations. Tests should therefore define tolerances that reflect the numerical behavior of the deployment environment.

Output postprocessing requires its own unit-level verification. Object detection software may decode bounding boxes, confidence values, class indices, and non-maximum suppression results, while segmentation software may convert logits into class masks. Pose or depth models can require coordinate transformations or scaling. Testing these operations separately helps distinguish neural-network inference defects from errors introduced by conventional software surrounding the model.

Threshold behavior should be tested at meaningful boundaries. Confidence scores immediately below, equal to, and above a configured detection threshold can verify whether filtering semantics are implemented correctly. Similar tests can examine intersection-over-union thresholds, minimum depth values, range gates, or segmentation confidence criteria. Boundary-focused tests are particularly useful because comparison-operator errors can remain hidden during normal model evaluation.

Tests should also verify empty and low-confidence outputs. A valid perception model may legitimately detect no objects or produce no result that satisfies a configured threshold. The software should return a well-defined empty representation rather than generating invalid indices, null dereferences, stale detections, or exceptions. Downstream robotics components often depend on this distinction between a valid empty observation and an inference failure.

Batch handling deserves explicit verification when the deployment interface supports multiple inputs. Tests should confirm that batch dimensions are interpreted correctly, outputs remain associated with the corresponding input samples, and single-sample operation remains valid. Dynamic batch sizes should be checked against the model contract because assumptions introduced during optimization or deployment conversion may differ from those used during model training.

Failure-path tests should exercise corrupted input, unavailable model resources, inference backend errors, memory allocation failures where they can be represented safely, and unexpected output dimensions. The inference layer should convert such failures into defined software states or exceptions that higher-level components can handle. A perception pipeline should never reuse an old detection silently simply because the current inference invocation failed.

Numerical validity is another important property. Output tensors should be checked for NaN, infinity, invalid probabilities, impossible coordinates, or values outside defined physical ranges when such restrictions apply. These checks are particularly useful after model conversion, quantization, or accelerator optimization because a technically successful inference call does not guarantee that the returned tensor contains meaningful numerical values.

CPU, GPU, and accelerator backends may require compatibility-oriented unit tests when the same perception component supports several execution targets. The purpose is not to benchmark their performance but to verify that each supported backend accepts the defined model and input contract and returns structurally compatible results. Numerical tolerances may differ between FP32, FP16, INT8, or other optimized representations and should be defined accordingly.

Quantized models require additional attention because preprocessing scales, zero points, calibration assumptions, and output dequantization can introduce implementation errors outside the neural network itself. Unit tests can use controlled numerical inputs to verify quantization and dequantization paths independently. This provides a simple method for detecting deployment conversion defects before they appear as unexplained degradation in robot perception performance.

Inference unit testing should distinguish software correctness from model-quality evaluation. A test confirming that an object detector returns tensors with correct shapes and correctly decoded boxes does not establish adequate detection accuracy, robustness, or generalization. Metrics such as mAP, IoU, localization error, OOD robustness, and task-level performance belong to broader AI model evaluation and benchmarking activities rather than basic inference unit verification.

Synthetic inputs are useful when they test software contracts, but they should not be mistaken for realistic perception validation. Constant images, zero tensors, structured point sets, and manually constructed logits can precisely exercise preprocessing and postprocessing functions. Recorded real sensor samples can complement these cases for regression purposes, while large datasets and scenario distributions are better handled in dedicated model-evaluation and system-validation pipelines.

Inference tests should remain independent of unnecessary middleware and hardware timing. If the objective is to verify preprocessing, model invocation, and output decoding, the test should call those functions directly rather than waiting for camera topics or ROS 2 executors. Communication behavior can then be tested separately during node integration, preserving a clear boundary between fast perception unit tests and more complex software integration tests.

Continuous integration turns these tests into safeguards against model and software changes. Updating an inference engine, model artifact, preprocessing library, accelerator runtime, or postprocessing implementation can automatically trigger reference tests. Failures then reveal incompatible tensor contracts, changed numerical behavior, missing resources, or decoding regressions before the modified perception stack reaches simulation, HIL, or robot deployment.

A well-designed perception inference unit-test suite therefore verifies the complete software contract immediately surrounding an AI model without attempting to prove the model\'s overall intelligence. By controlling inputs, validating preprocessing, checking inference interfaces, examining numerical outputs, testing postprocessing, and exercising failure paths, the suite provides fast and reproducible evidence that the deployed perception model is being executed and interpreted correctly.

인지 모델 추론(Perception Model Inference)은 원시 센서 관측값(Raw Sensor Observation)과 로봇이 수행하는 상위 수준 의사결정(Higher-Level Decision) 사이의 중요한 소프트웨어 경계이다. 이 경계에서 수행하는 단위 테스트(Unit Testing)는 인지 구성요소가 전체 ROS 2 그래프 또는 실제 로봇의 일부로 평가되기 전에 모델 로딩(Model Loading), 입력 준비(Input Preparation), 추론 실행(Inference Execution), 출력 해석(Output Interpretation), 실패 처리(Failure Handling)가 일관되게 동작하는지를 검증한다. 이러한 테스트 계층은 보다 광범위한 소프트웨어 단위 및 통합 테스트(Software Unit and Integration Testing) 구조에 포함된다.

추론 단위 테스트(Inference Unit Test)는 배포된 모델(Deployed Model)을 둘러싼 실행 경로를 실용적으로 가능한 가장 작은 범위로 격리해야 한다. 테스트에서는 결정론적인 이미지, 포인트 클라우드 텐서(Point Cloud Tensor), 깊이 맵(Depth Map), 특징 벡터(Feature Vector) 또는 기타 사전 정의된 입력을 추론 인터페이스에 직접 제공하고 결과 출력을 검사할 수 있다. 카메라 드라이버, ROS 2 전송, 네트워크 서비스 및 물리적 센서는 일반적으로 이 테스트 경계 밖에 두어 실패 원인을 추론 소프트웨어에 명확하게 한정할 수 있도록 해야 한다.

모델 초기화(Model Initialization)는 가장 먼저 검증해야 할 동작 중 하나이다. 테스트에서는 유효한 모델 아티팩트(Model Artifact)가 정상적으로 로딩되는지, 필요한 입력 및 출력 바인딩(Input and Output Binding)이 존재하는지, 예상된 텐서 차원(Tensor Dimension)이 인식되는지, 추론 객체가 사용 가능한 상태에 도달하는지를 확인해야 한다. 잘못된 모델 경로, 호환되지 않는 아티팩트, 누락된 메타데이터, 지원되지 않는 텐서 형상(Tensor Shape), 초기화 실패는 이후 실행 과정에서 정의되지 않은 동작을 발생시키는 대신 명시적인 오류를 생성해야 한다.

입력 전처리(Input Preprocessing)는 작은 전처리 차이도 AI 모델 출력에 상당한 변화를 발생시킬 수 있으므로 독립적으로 테스트해야 한다. 이미지 크기 조정(Resizing), 자르기(Cropping), 정규화(Normalization), 채널 순서(Channel Ordering), 색상 변환(Color Conversion), 텐서 레이아웃(Tensor Layout), 데이터 타입 변환(Datatype Conversion)은 제어된 입력에 대해 알려진 결과를 생성해야 한다. 라이다 또는 깊이 모델에서도 데이터가 네트워크에 입력되기 전에 좌표 정규화, 거리 필터링(Range Filtering), 복셀화(Voxelization), 패딩(Padding), 포인트 샘플링(Point Sampling)을 유사한 방식으로 검증할 수 있다.

텐서 형상 및 데이터 타입 검증(Tensor Shape and Datatype Validation)은 중요한 방어적 경계(Defensive Boundary)를 제공한다. 테스트에서는 올바른 형상의 텐서뿐만 아니라 차원이 누락된 입력, 예상하지 못한 배치 크기(Batch Size), 호환되지 않는 채널 수, 지원되지 않는 수치 데이터 타입을 제공해야 한다. 추론 래퍼(Inference Wrapper)는 계약에 따라 지원되는 입력을 변환하거나 잘못된 데이터를 명확하게 거부해야 한다. 잘못된 형상의 텐서를 아무런 경고 없이 재해석하면 그럴듯하지만 위험할 정도로 잘못된 인지 결과가 생성될 수 있다.

결정론적인 기준 입력(Deterministic Reference Input)은 회귀 테스트(Regression Testing)에 유용하다. 고정된 소수의 센서 샘플을 동일한 배포 모델 버전에 입력하고 그 출력을 저장된 기준 특성(Reference Characteristic)과 비교할 수 있다. GPU 커널, 최적화 백엔드(Optimization Backend), 수치 정밀도(Numerical Precision)에 따라 작은 차이가 발생할 수 있으므로 항상 정확한 동일성을 요구하는 것은 적절하지 않을 수 있다. 따라서 테스트에서는 배포 환경의 수치적 동작을 반영하는 허용오차(Tolerance)를 정의해야 한다.

출력 후처리(Output Postprocessing)도 별도의 단위 수준 검증이 필요하다. 객체 탐지(Object Detection) 소프트웨어는 바운딩 박스(Bounding Box), 신뢰도 값(Confidence Value), 클래스 인덱스(Class Index), 비최대 억제(Non-Maximum Suppression) 결과를 디코딩할 수 있으며, 분할(Segmentation) 소프트웨어는 로짓(Logit)을 클래스 마스크(Class Mask)로 변환할 수 있다. 자세 또는 깊이 모델은 좌표 변환이나 스케일링(Scaling)이 필요할 수 있다. 이러한 연산을 개별적으로 테스트하면 신경망 추론 결함과 모델 주변의 일반 소프트웨어에서 발생한 오류를 구분하는 데 도움이 된다.

임계값 동작(Threshold Behavior)은 의미 있는 경계값을 중심으로 테스트해야 한다. 설정된 탐지 임계값보다 바로 낮은 신뢰도 점수, 정확히 같은 점수, 바로 높은 점수를 사용하면 필터링 의미론(Filtering Semantics)이 올바르게 구현되었는지 검증할 수 있다. 이와 유사하게 교집합 대비 합집합(IoU, Intersection over Union) 임계값, 최소 깊이 값, 거리 게이트(Range Gate), 분할 신뢰도 기준을 검사할 수 있다. 경계 중심 테스트는 비교 연산자 오류가 일반적인 모델 평가 과정에서 발견되지 않고 남아 있는 문제를 탐지하는 데 특히 유용하다.

테스트에서는 비어 있는 출력(Empty Output)과 낮은 신뢰도의 출력도 검증해야 한다. 유효한 인지 모델이라도 객체를 전혀 탐지하지 못하거나 설정된 임계값을 만족하는 결과를 생성하지 않을 수 있다. 이러한 경우 소프트웨어는 잘못된 인덱스, 널 포인터 역참조(Null Dereference), 이전 탐지 결과(Stale Detection), 예외를 발생시키는 대신 명확하게 정의된 빈 표현(Empty Representation)을 반환해야 한다. 하위 로보틱스 구성요소는 유효하지만 비어 있는 관측과 추론 실패를 구분해야 하는 경우가 많다.

배포 인터페이스가 여러 입력을 지원하는 경우 배치 처리(Batch Handling)를 명시적으로 검증해야 한다. 테스트에서는 배치 차원이 올바르게 해석되는지, 출력이 해당 입력 샘플과 정확하게 연결되는지, 단일 샘플 동작도 정상적으로 유지되는지 확인해야 한다. 동적 배치 크기(Dynamic Batch Size)는 모델 계약과 비교하여 검증해야 한다. 최적화 또는 배포 변환 과정에서 도입된 가정이 모델 학습 단계에서 사용한 가정과 다를 수 있기 때문이다.

실패 경로 테스트(Failure-Path Test)는 손상된 입력, 사용할 수 없는 모델 리소스, 추론 백엔드 오류, 안전하게 표현할 수 있는 경우의 메모리 할당 실패, 예상하지 못한 출력 차원 등을 검사해야 한다. 추론 계층은 이러한 실패를 상위 수준 구성요소가 처리할 수 있는 정의된 소프트웨어 상태 또는 예외(Exception)로 변환해야 한다. 현재 추론 호출이 실패했다는 이유만으로 인지 파이프라인이 이전 탐지 결과를 아무런 표시 없이 재사용해서는 안 된다.

수치적 유효성(Numerical Validity)도 중요한 특성이다. 출력 텐서에서 NaN, 무한대(Infinity), 잘못된 확률값, 불가능한 좌표 또는 해당 제한이 적용되는 경우 정의된 물리적 범위를 벗어난 값을 검사해야 한다. 이러한 검사는 모델 변환(Model Conversion), 양자화(Quantization), 가속기 최적화(Accelerator Optimization) 이후 특히 유용하다. 기술적으로 추론 호출이 성공했다는 사실만으로 반환된 텐서가 의미 있는 수치값을 포함한다고 보장할 수는 없기 때문이다.

동일한 인지 구성요소가 여러 실행 대상을 지원한다면 CPU, GPU 및 가속기(Accelerator) 백엔드에 대한 호환성 중심 단위 테스트가 필요할 수 있다. 이러한 테스트의 목적은 성능을 벤치마킹하는 것이 아니라 지원되는 각 백엔드가 정의된 모델 및 입력 계약을 수용하고 구조적으로 호환되는 결과를 반환하는지 검증하는 것이다. FP32, FP16, INT8 또는 기타 최적화된 표현 사이에는 수치적 차이가 존재할 수 있으므로 각각에 적합한 허용오차를 정의해야 한다.

양자화 모델(Quantized Model)은 전처리 스케일(Preprocessing Scale), 제로 포인트(Zero Point), 보정 가정(Calibration Assumption), 출력 역양자화(Output Dequantization)가 신경망 자체 외부에서 구현 오류를 발생시킬 수 있으므로 추가적인 주의가 필요하다. 단위 테스트에서는 제어된 수치 입력을 이용하여 양자화 및 역양자화 경로를 독립적으로 검증할 수 있다. 이를 통해 로봇의 인지 성능 저하로 나타나기 전에 배포 변환 과정의 결함을 탐지할 수 있다.

추론 단위 테스트는 소프트웨어 정확성(Software Correctness)과 모델 품질 평가(Model-Quality Evaluation)를 구분해야 한다. 객체 탐지기가 올바른 형상의 텐서를 반환하고 바운딩 박스를 정확하게 디코딩하는지를 확인하는 테스트만으로 충분한 탐지 정확도, 강건성(Robustness), 일반화(Generalization)를 입증할 수는 없다. 평균 정밀도(mAP), 교집합 대비 합집합(IoU), 위치 오차(Localization Error), 분포 외 강건성(OOD Robustness), 작업 수준 성능(Task-Level Performance)과 같은 지표는 기본적인 추론 단위 검증이 아니라 보다 광범위한 AI 모델 평가 및 벤치마킹 활동에서 다루어야 한다.

합성 입력(Synthetic Input)은 소프트웨어 계약을 테스트하는 데 유용하지만 현실적인 인지 검증으로 간주해서는 안 된다. 일정한 이미지, 제로 텐서(Zero Tensor), 구조화된 포인트 집합, 수동으로 구성한 로짓을 사용하면 전처리 및 후처리 함수를 정밀하게 검사할 수 있다. 기록된 실제 센서 샘플을 이러한 사례에 추가하여 회귀 테스트에 활용할 수 있으며, 대규모 데이터셋과 시나리오 분포(Scenario Distribution)는 전용 모델 평가 및 시스템 검증 파이프라인에서 처리하는 것이 적절하다.

추론 테스트는 불필요한 미들웨어 및 하드웨어 타이밍과 독립적으로 유지해야 한다. 검증 목적이 전처리, 모델 호출(Model Invocation), 출력 디코딩이라면 카메라 토픽(Camera Topic)이나 ROS 2 실행기(Executor)를 기다리는 대신 해당 함수를 직접 호출해야 한다. 이후 통신 동작은 노드 통합(Node Integration) 과정에서 별도로 테스트할 수 있으며, 이를 통해 빠른 인지 단위 테스트와 복잡한 소프트웨어 통합 테스트 사이의 명확한 경계를 유지할 수 있다.

지속적 통합(CI, Continuous Integration)은 이러한 테스트를 모델 및 소프트웨어 변경에 대한 보호 장치로 전환한다. 추론 엔진(Inference Engine), 모델 아티팩트, 전처리 라이브러리, 가속기 런타임(Accelerator Runtime), 후처리 구현이 변경되면 기준 테스트(Reference Test)를 자동으로 실행할 수 있다. 테스트 실패를 통해 변경된 인지 스택이 시뮬레이션(Simulation), 하드웨어 인더루프(HIL), 실제 로봇 배포 단계에 도달하기 전에 호환되지 않는 텐서 계약, 변경된 수치 동작, 누락된 리소스 또는 디코딩 회귀를 발견할 수 있다.

잘 설계된 인지 추론 단위 테스트 스위트(Perception Inference Unit-Test Suite)는 AI 모델의 전체적인 지능을 입증하려는 것이 아니라 AI 모델을 직접 둘러싼 완전한 소프트웨어 계약(Software Contract)을 검증한다. 입력을 제어하고, 전처리를 검증하며, 추론 인터페이스를 확인하고, 수치 출력을 검사하며, 후처리와 실패 경로를 테스트함으로써 배포된 인지 모델이 올바르게 실행되고 해석되고 있다는 빠르고 재현 가능한 검증 증거를 제공한다.

##  

## 02.06. Integration Test ROS2 Node Graph [w/Code]

![](images/image6.png){width="7.268055555555556in" height="7.268055555555556in"}

ROS 2 node-graph integration testing verifies that independently tested software components operate correctly when connected through the middleware mechanisms used by the robot. Unlike unit tests that isolate algorithms or classes, these tests intentionally exercise publishers, subscribers, services, actions, parameters, executors, and lifecycle interactions. Within the chapter structure, this stage follows component-level unit testing and precedes broader end-to-end software integration testing.

A node graph represents the runtime relationships among ROS 2 nodes and their communication interfaces. An integration test constructs a controlled subset of this graph, launches the required nodes, injects known inputs, and observes messages or state transitions at defined outputs. The objective is not simply to prove that individual nodes start successfully, but to verify that interfaces between nodes satisfy the communication and behavioral contracts assumed by the overall robot software.

Topic integration testing verifies publisher-to-subscriber communication under realistic ROS 2 execution. A test publisher can inject deterministic sensor, command, state, or diagnostic messages while one or more production nodes process them. The test then observes downstream topics and checks message type, header information, values, timestamps, frame identifiers, and other application-specific fields against expected results.

Communication tests should account for ROS 2 Quality of Service(QoS) because compatible message types alone do not guarantee successful data exchange. Reliability, durability, history, queue depth, and deadline policies can influence whether endpoints communicate as intended. Integration tests should therefore use the QoS configurations expected in deployment and detect incompatible settings that might otherwise appear as unexplained message loss when the robot is assembled.

Service integration tests verify synchronous request-response contracts between nodes. The test can issue valid and invalid requests, confirm response fields, and evaluate behavior when the requested operation cannot be completed. Configuration services, mode changes, map queries, or device-management interfaces are suitable examples. Timeout and error behavior should be explicitly tested so a missing response does not cause an uncontrolled wait in dependent software.

ROS 2 actions require additional verification because they represent longer-running operations with goals, feedback, and final results. Integration tests can submit a known goal, observe intermediate feedback, and verify successful completion or rejection. Cancellation should also be tested where supported. Navigation, manipulation, docking, and trajectory execution commonly depend on these semantics, making action-state transitions important integration boundaries.

Parameter interactions should be verified when node behavior depends on configuration established during startup or changed dynamically. Tests can launch nodes with controlled parameter sets and confirm that the resulting behavior matches the configuration. Invalid values, missing parameters, dynamic updates, and parameter callbacks should be exercised according to the component contract, particularly when configuration influences limits, safety behavior, coordinate frames, or algorithm selection.

Lifecycle nodes introduce explicit state transitions such as unconfigured, inactive, active, and finalized states. Integration tests should verify that dependent communication begins only in appropriate states and that configure, activate, deactivate, cleanup, and shutdown transitions produce expected effects. Failed initialization should not leave a node appearing operational, and dependent nodes should respond predictably when a lifecycle-managed component becomes unavailable.

Launch-based testing is useful for constructing reproducible node graphs. Instead of requiring an engineer to start several terminals manually, a test launch description can start the required production nodes, supporting processes, and test components with known configuration. The test environment can then monitor process exit codes and communication behavior, allowing the same graph to execute on developer systems and continuous-integration workers.

Discovery and startup synchronization require deliberate handling. ROS 2 communication endpoints may need time to discover each other, so tests should avoid relying on arbitrary sleep intervals whenever possible. A more robust test waits for observable readiness conditions such as subscriber counts, available services, action servers, lifecycle states, or explicit initialization signals. This reduces flaky failures caused by differences in processor speed or CI workload.

Deterministic test data is essential for interpreting graph-level failures. Recorded or synthetic sensor messages can represent known robot states, obstacles, poses, trajectories, or commands. When identical inputs are injected, downstream outputs should satisfy predefined expectations within suitable numerical tolerances. The dataset should remain small enough for rapid execution while still exercising the interface behavior that distinguishes integration testing from isolated unit verification.

Timestamp and coordinate-frame consistency should receive particular attention because many robotics integration defects arise at these boundaries. Tests can verify that message timestamps remain logically ordered, stale inputs are rejected correctly, and frame identifiers match the expected coordinate system. When transform-dependent processing is involved, the test environment should provide controlled transformations so missing or inconsistent frames produce predictable diagnostic or failure behavior.

Fault injection expands integration testing beyond nominal message flow. A publisher can stop unexpectedly, a service can become unavailable, malformed data can be injected, or a component can report an internal fault. The surrounding node graph should react according to its design, such as suppressing commands, generating diagnostics, entering a degraded state, or waiting for recovery. These tests verify interactions that cannot be established by testing each node independently.

Integration tests should also examine message rates and queue behavior where correctness depends on continuous data flow. A perception or localization node may receive sensor messages faster than it can process them, while a controller may require state updates within a defined interval. Tests can introduce controlled publishing rates and verify that queue configuration, callback execution, and stale-data handling preserve the intended behavior without turning the test into a full performance benchmark.

Executors and callback groups can expose concurrency defects that do not appear during isolated unit testing. Multi-threaded execution may reveal race conditions, shared-state synchronization problems, callback ordering assumptions, or deadlocks. Integration tests should exercise the executor configuration used by the deployed component when concurrency is part of its architecture, while keeping test inputs deterministic enough that failures remain reproducible.

The test boundary should remain narrower than a complete robot system. A navigation-related integration test might include localization, planning, and command interfaces while replacing physical sensors and motor hardware with controlled sources and sinks. This allows ROS 2 communication and software composition to be tested without introducing hardware uncertainty. Complete physical behavior belongs to later simulation, HIL, system, and field-validation stages.

Pass and fail criteria should describe observable graph behavior rather than internal implementation details. Examples include receiving a valid command within a defined condition, rejecting an invalid request, reaching an expected lifecycle state, or ceasing command publication after input loss. Tests based on external contracts remain useful when nodes are internally refactored, whereas tests tightly coupled to private implementation details become unnecessarily fragile.

ROS 2 node-graph integration tests should be incorporated into continuous integration after fast unit tests have passed. The pipeline can build the workspace, launch controlled node groups, execute communication scenarios, collect test results, and terminate all processes cleanly. Because these tests require more middleware resources and execution time than unit tests, they can form a second verification layer before more expensive end-to-end, simulation, HIL, and physical testing.

A successful node-graph integration test does not prove that the entire robot will behave correctly in the real world. It establishes that selected ROS 2 components can discover each other, exchange compatible information, coordinate state, and handle defined faults under controlled software conditions. This evidence closes the gap between isolated unit correctness and complete software integration, providing a reproducible foundation for the subsequent end-to-end testing stage defined in the chapter structure.

ROS 2 노드 그래프 통합 테스트(ROS 2 Node-Graph Integration Testing)는 독립적으로 테스트된 소프트웨어 구성요소가 로봇에서 사용하는 미들웨어(Middleware) 메커니즘을 통해 연결되었을 때 올바르게 동작하는지를 검증한다. 알고리즘이나 클래스를 격리하는 단위 테스트(Unit Test)와 달리 이러한 테스트는 퍼블리셔(Publisher), 서브스크라이버(Subscriber), 서비스(Service), 액션(Action), 매개변수(Parameter), 실행기(Executor), 수명주기 상호작용(Lifecycle Interaction)을 의도적으로 검증한다. 이 장의 구조에서 이러한 단계는 구성요소 수준 단위 테스트 이후, 보다 광범위한 종단 간 소프트웨어 통합 테스트(End-to-End Software Integration Testing) 이전에 위치한다.

노드 그래프(Node Graph)는 ROS 2 노드와 해당 통신 인터페이스 사이의 런타임 관계(Runtime Relationship)를 나타낸다. 통합 테스트(Integration Test)는 이러한 그래프의 제어된 부분집합을 구성하고, 필요한 노드를 실행하며, 알려진 입력을 주입하고, 정의된 출력에서 메시지 또는 상태 전이(State Transition)를 관찰한다. 목적은 개별 노드가 성공적으로 시작되는지를 단순히 확인하는 것이 아니라 노드 사이의 인터페이스가 전체 로봇 소프트웨어에서 가정하는 통신 및 동작 계약(Communication and Behavioral Contract)을 충족하는지 검증하는 것이다.

토픽 통합 테스트(Topic Integration Testing)는 실제 ROS 2 실행 환경에서 퍼블리셔와 서브스크라이버 간 통신을 검증한다. 테스트 퍼블리셔(Test Publisher)는 결정론적인 센서, 명령, 상태 또는 진단 메시지를 주입할 수 있으며 하나 이상의 실제 운용 노드(Production Node)가 이를 처리한다. 이후 테스트는 하위 토픽(Downstream Topic)을 관찰하고 메시지 유형, 헤더 정보, 값, 타임스탬프(Timestamp), 프레임 식별자(Frame Identifier) 및 기타 응용 분야별 필드를 예상 결과와 비교한다.

통신 테스트에서는 호환되는 메시지 유형만으로 성공적인 데이터 교환이 보장되지 않기 때문에 ROS 2 서비스 품질(QoS, Quality of Service)을 고려해야 한다. 신뢰성(Reliability), 내구성(Durability), 히스토리(History), 큐 깊이(Queue Depth), 데드라인(Deadline) 정책은 통신 종단점(Endpoint)이 의도한 대로 통신할 수 있는지에 영향을 미친다. 따라서 통합 테스트에서는 실제 배포 환경에서 예상되는 QoS 구성을 사용하고, 로봇 시스템을 조립했을 때 원인을 알 수 없는 메시지 손실처럼 나타날 수 있는 비호환 설정을 탐지해야 한다.

서비스 통합 테스트(Service Integration Test)는 노드 사이의 동기식 요청-응답 계약(Synchronous Request-Response Contract)을 검증한다. 테스트에서는 유효하거나 잘못된 요청을 전달하고, 응답 필드를 확인하며, 요청된 작업을 완료할 수 없는 경우의 동작을 평가할 수 있다. 구성 서비스(Configuration Service), 모드 변경, 지도 질의(Map Query), 장치 관리 인터페이스(Device-Management Interface) 등이 대표적인 사례이다. 응답이 없을 때 종속 소프트웨어가 무제한으로 대기하지 않도록 타임아웃 및 오류 동작도 명시적으로 테스트해야 한다.

ROS 2 액션(Action)은 목표(Goal), 피드백(Feedback), 최종 결과(Final Result)를 포함하는 장시간 실행 작업을 표현하므로 추가적인 검증이 필요하다. 통합 테스트에서는 알려진 목표를 제출하고, 중간 피드백을 관찰하며, 성공적인 완료 또는 거부 여부를 검증할 수 있다. 지원되는 경우 취소(Cancellation) 동작도 테스트해야 한다. 내비게이션(Navigation), 조작(Manipulation), 도킹(Docking), 궤적 실행(Trajectory Execution)은 이러한 의미론에 의존하는 경우가 많으므로 액션 상태 전이는 중요한 통합 경계가 된다.

노드 동작이 시작 시 설정되거나 동적으로 변경되는 구성에 의존하는 경우 매개변수 상호작용(Parameter Interaction)을 검증해야 한다. 테스트에서는 제어된 매개변수 집합으로 노드를 실행하고 결과 동작이 해당 구성과 일치하는지 확인할 수 있다. 잘못된 값, 누락된 매개변수, 동적 갱신(Dynamic Update), 매개변수 콜백(Parameter Callback)은 구성요소 계약에 따라 검증해야 하며, 특히 구성이 제한값, 안전 동작, 좌표 프레임 또는 알고리즘 선택에 영향을 미치는 경우 중요하다.

수명주기 노드(Lifecycle Node)는 미구성(Unconfigured), 비활성(Inactive), 활성(Active), 종료(Finalized)와 같은 명시적인 상태 전이를 도입한다. 통합 테스트에서는 종속 통신이 적절한 상태에서만 시작되는지 검증하고, 구성(Configure), 활성화(Activate), 비활성화(Deactivate), 정리(Cleanup), 종료(Shutdown) 전이가 예상된 결과를 생성하는지 확인해야 한다. 초기화 실패 후 노드가 정상 동작하는 것처럼 보여서는 안 되며, 수명주기로 관리되는 구성요소가 사용할 수 없는 상태가 되었을 때 종속 노드도 예측 가능한 방식으로 대응해야 한다.

실행 기반 테스트(Launch-Based Testing)는 재현 가능한 노드 그래프를 구성하는 데 유용하다. 엔지니어가 여러 터미널에서 노드를 수동으로 실행하는 대신 테스트 실행 정의(Test Launch Description)를 통해 필요한 실제 운용 노드, 지원 프로세스(Supporting Process), 테스트 구성요소를 알려진 구성으로 시작할 수 있다. 이후 테스트 환경은 프로세스 종료 코드(Process Exit Code)와 통신 동작을 감시하여 동일한 그래프를 개발자 시스템과 지속적 통합(CI, Continuous Integration) 작업 환경에서 반복 실행할 수 있다.

디스커버리 및 시작 동기화(Discovery and Startup Synchronization)는 의도적으로 처리해야 한다. ROS 2 통신 종단점이 서로를 발견하는 데 시간이 필요할 수 있으므로 가능한 경우 임의의 대기 시간(Sleep Interval)에 의존하지 않아야 한다. 보다 견고한 테스트는 서브스크라이버 수, 사용 가능한 서비스, 액션 서버(Action Server), 수명주기 상태 또는 명시적인 초기화 신호와 같이 관측 가능한 준비 조건(Readiness Condition)을 기다린다. 이를 통해 프로세서 속도 또는 CI 작업 부하 차이로 발생하는 불안정한 실패(Flaky Failure)를 줄일 수 있다.

결정론적 테스트 데이터(Deterministic Test Data)는 그래프 수준 실패를 해석하는 데 필수적이다. 기록되거나 합성된 센서 메시지는 알려진 로봇 상태, 장애물, 자세(Pose), 궤적 또는 명령을 표현할 수 있다. 동일한 입력을 주입했을 때 하위 출력은 적절한 수치 허용오차(Numerical Tolerance) 내에서 사전에 정의된 기대 결과를 만족해야 한다. 데이터셋은 빠르게 실행할 수 있을 만큼 작게 유지하면서도 통합 테스트와 격리된 단위 검증을 구분하는 인터페이스 동작을 충분히 검증할 수 있어야 한다.

타임스탬프 및 좌표 프레임 일관성(Timestamp and Coordinate-Frame Consistency)은 많은 로보틱스 통합 결함이 이러한 경계에서 발생하므로 특별한 주의가 필요하다. 테스트에서는 메시지 타임스탬프가 논리적인 순서를 유지하는지, 오래된 입력(Stale Input)이 올바르게 거부되는지, 프레임 식별자가 예상된 좌표계와 일치하는지 검증할 수 있다. 변환 의존 처리(Transform-Dependent Processing)가 포함되는 경우 테스트 환경은 제어된 변환(Controlled Transformation)을 제공하여 누락되거나 일관되지 않은 프레임이 예측 가능한 진단 또는 실패 동작을 발생시키도록 해야 한다.

결함 주입(Fault Injection)은 통합 테스트의 범위를 정상적인 메시지 흐름 이상으로 확장한다. 퍼블리셔가 예기치 않게 중단되거나, 서비스를 사용할 수 없게 되거나, 잘못 구성된 데이터(Malformed Data)가 주입되거나, 구성요소가 내부 결함을 보고하도록 만들 수 있다. 주변 노드 그래프는 설계에 따라 명령 억제(Command Suppression), 진단 정보 생성, 성능 저하 상태(Degraded State) 진입 또는 복구 대기와 같은 동작을 수행해야 한다. 이러한 테스트는 각 노드를 독립적으로 테스트하는 것만으로는 확인할 수 없는 상호작용을 검증한다.

정확성이 연속적인 데이터 흐름에 의존하는 경우 통합 테스트에서는 메시지 전송률(Message Rate)과 큐 동작(Queue Behavior)도 검사해야 한다. 인지 또는 위치 추정 노드는 처리 가능한 속도보다 빠르게 센서 메시지를 수신할 수 있으며, 제어기는 정의된 시간 간격 내에 상태 갱신을 요구할 수 있다. 테스트에서는 제어된 발행 주기(Publishing Rate)를 적용하고 큐 구성, 콜백 실행(Callback Execution), 오래된 데이터 처리가 전체 성능 벤치마크로 확대되지 않는 범위에서 의도된 동작을 유지하는지 검증할 수 있다.

실행기(Executor)와 콜백 그룹(Callback Group)은 격리된 단위 테스트에서 나타나지 않는 동시성 결함(Concurrency Defect)을 노출할 수 있다. 멀티스레드 실행(Multi-Threaded Execution)은 경쟁 상태(Race Condition), 공유 상태 동기화 문제, 콜백 실행 순서에 대한 잘못된 가정 또는 교착 상태(Deadlock)를 드러낼 수 있다. 동시성이 아키텍처의 일부인 경우 통합 테스트에서는 실제 배포 구성요소가 사용하는 실행기 구성을 검증하면서도 실패를 재현할 수 있을 정도로 테스트 입력의 결정성을 유지해야 한다.

테스트 경계(Test Boundary)는 완전한 로봇 시스템보다 좁게 유지해야 한다. 예를 들어 내비게이션 관련 통합 테스트에는 위치 추정(Localization), 경로 계획(Planning), 명령 인터페이스를 포함하면서 물리적 센서와 모터 하드웨어를 제어된 입력원(Source)과 출력 수신부(Sink)로 대체할 수 있다. 이를 통해 하드웨어 불확실성을 도입하지 않고 ROS 2 통신 및 소프트웨어 구성(Software Composition)을 테스트할 수 있다. 완전한 물리적 동작은 이후 시뮬레이션(Simulation), 하드웨어 인더루프(HIL, Hardware-in-the-Loop), 시스템 테스트(System Test), 현장 검증(Field Validation) 단계에서 다루어야 한다.

합격 및 불합격 기준(Pass and Fail Criteria)은 내부 구현 세부사항보다 관측 가능한 그래프 동작(Observable Graph Behavior)을 설명해야 한다. 정의된 조건에서 유효한 명령을 수신하는 것, 잘못된 요청을 거부하는 것, 예상된 수명주기 상태에 도달하는 것, 입력 손실 이후 명령 발행을 중단하는 것 등이 대표적인 사례이다. 외부 계약(External Contract)을 기반으로 작성된 테스트는 노드 내부가 리팩터링(Refactoring)되더라도 계속 유효하지만, 비공개 구현 세부사항에 과도하게 결합된 테스트는 불필요하게 취약해진다.

ROS 2 노드 그래프 통합 테스트는 빠른 단위 테스트가 통과한 이후 지속적 통합(CI)에 포함해야 한다. 파이프라인은 작업공간(Workspace)을 빌드하고, 제어된 노드 그룹을 실행하며, 통신 시나리오를 수행하고, 테스트 결과를 수집한 후 모든 프로세스를 정상적으로 종료할 수 있다. 이러한 테스트는 단위 테스트보다 더 많은 미들웨어 리소스와 실행 시간을 요구하므로 비용이 높은 종단 간 테스트, 시뮬레이션, HIL 및 물리적 테스트 이전의 두 번째 검증 계층으로 구성할 수 있다.

성공적인 노드 그래프 통합 테스트만으로 전체 로봇이 실제 환경에서 올바르게 동작한다는 것을 입증할 수는 없다. 그러나 선택된 ROS 2 구성요소가 서로를 발견하고, 호환되는 정보를 교환하며, 상태를 조정하고, 제어된 소프트웨어 조건에서 정의된 결함을 처리할 수 있다는 것을 입증한다. 이러한 검증 증거는 격리된 단위 수준의 정확성과 완전한 소프트웨어 통합 사이의 간극을 연결하며, 이 장의 구조에서 다음 단계로 정의된 종단 간 테스트(End-to-End Testing)를 위한 재현 가능한 기반을 제공한다.

##  

## 02.07. End to End SW Integration Test Framework [w/Code]

![](images/image7.png){width="7.268055555555556in" height="7.268055555555556in"}

End-to-end software integration testing verifies complete functional paths across multiple robot software subsystems after unit-level and ROS 2 node-graph integration tests have established lower-level correctness. Instead of testing one class, node, or communication interface, an end-to-end framework follows information from an external input or mission request through perception, state estimation, planning, control, and supporting services to an observable software output.

The test boundary should represent a meaningful robot workflow while remaining controllable and reproducible. For an autonomous mobile robot, a scenario may begin with a navigation goal and predefined sensor observations, pass through localization and path planning, and terminate at generated motion commands. A manipulation scenario may begin with an object observation and task request and continue through pose estimation, grasp planning, trajectory generation, and controller command output.

An effective framework separates test orchestration from the production software being evaluated. The orchestration layer prepares configuration, launches required processes, injects test data, observes system outputs, applies pass or fail criteria, and performs cleanup. Production nodes should execute with configurations that closely represent deployment so the test evaluates actual software composition rather than a special implementation created only for testing.

Scenario definitions provide the primary abstraction for end-to-end testing. Each scenario describes an initial state, required configuration, input events, expected intermediate conditions, final success criteria, and timeout behavior. A navigation scenario might define a starting pose, map, goal, and obstacle sequence, while the expected outcome specifies whether a valid trajectory and safe command stream must be produced within defined constraints.

Input sources should be deterministic whenever possible. Synthetic messages, recorded sensor sequences, predefined maps, database fixtures, or controlled service responses can reproduce a known operating condition without physical hardware. The same scenario should produce equivalent conclusions when executed repeatedly. Deterministic inputs make regression failures easier to diagnose and allow the framework to compare software versions under identical conditions.

End-to-end tests should validate intermediate checkpoints as well as final outputs. A robot may eventually produce a command even though localization briefly became invalid or planning generated an unsafe intermediate state. Observing key states across the pipeline allows failures to be localized more effectively. Checkpoints can include valid localization, perception output availability, successful plan generation, controller activation, diagnostics, and expected lifecycle states.

ROS 2 communication remains an important part of the execution path. Topics, services, actions, parameters, lifecycle transitions, transforms, and executors should operate as they do in the target software architecture. Unlike isolated node-graph tests, however, the objective is not to verify each interface independently. The framework verifies that multiple interfaces cooperate correctly to complete a higher-level robot function from beginning to end.

Launch orchestration should manage all required software processes predictably. The framework needs to start components in the correct dependency order, determine when they are ready, execute the scenario, and terminate them cleanly. Readiness should preferably be based on observable conditions such as lifecycle states, service availability, action-server availability, or required topic connections rather than fixed sleep periods that can cause flaky tests.

Timeout management prevents a failed workflow from blocking the entire test campaign. Each scenario should define reasonable limits for initialization, communication, planning, execution, and shutdown where appropriate. A timeout is itself an observable failure condition and should generate diagnostic evidence showing which expected event did not occur. This makes stalled software paths distinguishable from incorrect numerical outputs or explicit process failures.

System-level assertions should focus on externally meaningful behavior. A navigation pipeline can be required to produce bounded velocity commands only after localization is valid, while a manipulation pipeline can be required to reject an unreachable target without issuing unsafe actuator commands. Such assertions remain useful even when internal algorithms are replaced because they describe the functional contract of the integrated software rather than private implementation details.

Failure injection is essential for verifying robustness across subsystem boundaries. The framework can stop a perception stream, delay localization updates, return a failed planning result, disconnect a supporting service, or inject invalid state data. The integrated system should react according to its design by suppressing commands, retrying an operation, entering a degraded mode, reporting diagnostics, or transitioning to a defined safe state.

Data collection should be integrated into the framework rather than added manually after a failure. Test execution can preserve logs, ROS 2 messages, diagnostic events, process exit codes, parameter snapshots, timestamps, and scenario metadata. These artifacts make failures reproducible and provide evidence for regression analysis. A failed CI run should contain enough information for an engineer to identify the affected stage without rerunning the complete scenario interactively.

Test isolation is necessary because end-to-end scenarios involve substantial shared state. Temporary maps, configuration files, databases, caches, namespaces, ports, and generated outputs should be separated between test runs. Processes from a previous scenario must not remain active and influence subsequent execution. Reliable cleanup is therefore part of the framework itself rather than an optional convenience after a successful test.

Environment reproducibility becomes increasingly important as the integration scope grows. Container images, pinned dependencies, known ROS 2 configurations, controlled model artifacts, and versioned test datasets can reduce differences between developer machines and CI workers. The software revision, configuration revision, test-data version, and relevant runtime dependencies should be traceable so a historical failure can be reconstructed when necessary.

Parallel execution can reduce test duration, but scenarios should be parallelized only when resources and namespaces are sufficiently isolated. Multiple ROS 2 graphs may otherwise interfere through discovery, shared network resources, databases, GPU allocation, or fixed device names. Resource-aware scheduling is particularly important when perception models or computationally expensive planners compete for accelerators and memory on the same test worker.

Performance observations can be collected during end-to-end execution without turning every scenario into a benchmark. The framework may record processing latency, message age, dropped updates, planning duration, or resource usage and compare them with broad regression thresholds. Strict performance certification should remain a separate activity, but large changes in timing can provide early evidence of integration problems that functional pass or fail checks alone may miss.

The framework should support both positive and negative scenarios. Positive tests verify that valid requests can complete successfully, while negative tests verify that invalid, unavailable, or unsafe conditions are rejected correctly. A mature suite includes nominal workflows, boundary cases, recovery paths, and representative failures so software integration is evaluated not only by its ability to succeed but also by its ability to fail safely.

Continuous integration should execute end-to-end tests after faster unit and focused integration suites have passed. This ordering avoids consuming expensive resources on software that already violates lower-level contracts. Selected smoke scenarios can run on every change, while broader regression suites can run on scheduled or release-oriented pipelines. Test results should remain machine-readable so failures can be tracked across software revisions.

End-to-end software integration testing still does not replace simulation, HIL, or field validation. Controlled software inputs cannot fully reproduce physical dynamics, sensor uncertainty, actuator behavior, environmental variability, or real-time hardware interactions. Instead, this framework establishes that the integrated software stack can execute complete robot workflows coherently before those workflows are exposed to increasingly realistic and expensive verification environments.

A well-designed end-to-end framework therefore connects component correctness with system-level software behavior. By combining reproducible scenarios, controlled inputs, production-like ROS 2 composition, intermediate checkpoints, failure injection, automated evidence collection, and CI execution, it provides a repeatable method for determining whether the robot software stack operates as one coordinated system before verification progresses to APIs, data pipelines, HIL, simulation, and physical testing.

종단 간 소프트웨어 통합 테스트(End-to-End Software Integration Testing)는 단위 수준 테스트와 ROS 2 노드 그래프 통합 테스트(ROS 2 Node-Graph Integration Test)를 통해 하위 수준의 정확성이 확보된 이후 여러 로봇 소프트웨어 하위 시스템에 걸쳐 완전한 기능 경로(Functional Path)를 검증한다. 하나의 클래스, 노드 또는 통신 인터페이스만 테스트하는 대신 외부 입력이나 임무 요청(Mission Request)이 인지(Perception), 상태 추정(State Estimation), 계획(Planning), 제어(Control), 지원 서비스를 거쳐 관측 가능한 소프트웨어 출력으로 전달되는 전체 과정을 추적한다.

테스트 경계(Test Boundary)는 제어 가능성과 재현성을 유지하면서 의미 있는 로봇 작업 흐름(Robot Workflow)을 표현해야 한다. 자율이동로봇(AMR, Autonomous Mobile Robot)의 경우 내비게이션 목표(Navigation Goal)와 사전에 정의된 센서 관측에서 시나리오를 시작하여 위치 추정(Localization)과 경로 계획(Path Planning)을 거쳐 최종적으로 생성된 모션 명령(Motion Command)에서 종료할 수 있다. 조작(Manipulation) 시나리오는 객체 관측과 작업 요청에서 시작하여 자세 추정(Pose Estimation), 파지 계획(Grasp Planning), 궤적 생성(Trajectory Generation), 제어기 명령 출력까지 이어질 수 있다.

효과적인 프레임워크(Framework)는 테스트 오케스트레이션(Test Orchestration)을 평가 대상 실제 운용 소프트웨어(Production Software)와 분리한다. 오케스트레이션 계층은 구성(Configuration)을 준비하고, 필요한 프로세스를 실행하며, 테스트 데이터를 주입하고, 시스템 출력을 관찰하며, 합격 또는 불합격 기준(Pass or Fail Criteria)을 적용하고, 종료 후 정리(Cleanup)를 수행한다. 실제 운용 노드는 배포 환경을 최대한 가깝게 반영하는 구성으로 실행하여 테스트만을 위해 특별히 제작된 구현이 아니라 실제 소프트웨어 구성을 평가해야 한다.

시나리오 정의(Scenario Definition)는 종단 간 테스트의 핵심 추상화(Abstraction)를 제공한다. 각 시나리오는 초기 상태, 필요한 구성, 입력 이벤트(Input Event), 예상 중간 조건, 최종 성공 기준, 타임아웃 동작(Timeout Behavior)을 기술한다. 예를 들어 내비게이션 시나리오는 시작 자세, 지도, 목표, 장애물 시퀀스(Obstacle Sequence)를 정의할 수 있으며, 예상 결과에서는 정의된 제약조건 내에서 유효한 궤적과 안전한 명령 스트림(Command Stream)이 생성되어야 하는지를 지정할 수 있다.

가능한 경우 입력원(Input Source)은 결정론적(Deterministic)이어야 한다. 합성 메시지(Synthetic Message), 기록된 센서 시퀀스, 사전에 정의된 지도, 데이터베이스 픽스처(Database Fixture), 제어된 서비스 응답을 사용하면 물리적 하드웨어 없이도 알려진 운용 조건을 재현할 수 있다. 동일한 시나리오는 반복 실행에서도 동등한 결론을 생성해야 한다. 결정론적인 입력은 회귀 실패(Regression Failure)의 진단을 쉽게 만들고 동일한 조건에서 서로 다른 소프트웨어 버전을 비교할 수 있도록 한다.

종단 간 테스트는 최종 출력뿐만 아니라 중간 체크포인트(Intermediate Checkpoint)도 검증해야 한다. 로봇이 최종적으로 명령을 생성했더라도 그 과정에서 위치 추정이 일시적으로 유효하지 않았거나 경로 계획이 위험한 중간 상태를 생성했을 수 있다. 파이프라인 전체의 주요 상태를 관찰하면 실패 원인을 더욱 효과적으로 국소화할 수 있다. 체크포인트에는 유효한 위치 추정, 인지 출력의 가용성, 성공적인 경로 생성, 제어기 활성화, 진단 정보 및 예상된 수명주기 상태(Lifecycle State) 등이 포함될 수 있다.

ROS 2 통신은 전체 실행 경로에서 여전히 중요한 부분을 차지한다. 토픽(Topic), 서비스(Service), 액션(Action), 매개변수(Parameter), 수명주기 전이(Lifecycle Transition), 변환(Transform), 실행기(Executor)는 목표 소프트웨어 아키텍처에서 동작하는 방식과 동일하게 작동해야 한다. 그러나 격리된 노드 그래프 테스트와 달리 목적은 각각의 인터페이스를 독립적으로 검증하는 것이 아니다. 프레임워크는 여러 인터페이스가 협력하여 상위 수준의 로봇 기능을 처음부터 끝까지 올바르게 완료하는지를 검증한다.

실행 오케스트레이션(Launch Orchestration)은 필요한 모든 소프트웨어 프로세스를 예측 가능한 방식으로 관리해야 한다. 프레임워크는 올바른 의존성 순서에 따라 구성요소를 시작하고, 준비 완료 여부를 판단하며, 시나리오를 실행하고, 이후 모든 구성요소를 정상적으로 종료할 수 있어야 한다. 준비 상태(Readiness)는 불안정한 테스트(Flaky Test)를 발생시킬 수 있는 고정된 대기 시간보다 수명주기 상태, 서비스 가용성, 액션 서버(Action Server) 가용성 또는 필요한 토픽 연결과 같은 관측 가능한 조건을 기반으로 판단하는 것이 바람직하다.

타임아웃 관리(Timeout Management)는 실패한 작업 흐름이 전체 테스트 캠페인을 차단하는 것을 방지한다. 각 시나리오는 필요한 경우 초기화, 통신, 계획, 실행, 종료에 대한 합리적인 시간 제한을 정의해야 한다. 타임아웃 자체도 관측 가능한 실패 조건이며, 어떤 예상 이벤트가 발생하지 않았는지를 보여주는 진단 증거(Diagnostic Evidence)를 생성해야 한다. 이를 통해 정지된 소프트웨어 경로를 잘못된 수치 출력이나 명시적인 프로세스 실패와 구분할 수 있다.

시스템 수준 어설션(System-Level Assertion)은 외부에서 의미 있게 관측할 수 있는 동작에 초점을 맞춰야 한다. 내비게이션 파이프라인은 위치 추정이 유효해진 이후에만 제한 범위 내의 속도 명령을 생성하도록 요구할 수 있으며, 조작 파이프라인은 도달할 수 없는 목표를 안전하지 않은 액추에이터 명령 없이 거부하도록 요구할 수 있다. 이러한 어설션은 내부 알고리즘이 교체되더라도 유효한데, 이는 비공개 구현 세부사항이 아니라 통합된 소프트웨어의 기능적 계약(Functional Contract)을 설명하기 때문이다.

결함 주입(Failure Injection)은 하위 시스템 경계를 넘어 강건성(Robustness)을 검증하는 데 필수적이다. 프레임워크는 인지 데이터 스트림을 중단하거나, 위치 추정 갱신을 지연시키거나, 경로 계획 실패 결과를 반환하거나, 지원 서비스를 연결 해제하거나, 잘못된 상태 데이터를 주입할 수 있다. 통합 시스템은 설계에 따라 명령을 억제하고, 작업을 재시도하거나, 성능 저하 모드(Degraded Mode)로 진입하고, 진단 정보를 보고하거나, 정의된 안전 상태(Safe State)로 전환해야 한다.

데이터 수집(Data Collection)은 실패가 발생한 이후 수동으로 추가하는 것이 아니라 프레임워크에 통합되어야 한다. 테스트 실행 과정에서 로그(Log), ROS 2 메시지, 진단 이벤트(Diagnostic Event), 프로세스 종료 코드, 매개변수 스냅샷(Parameter Snapshot), 타임스탬프, 시나리오 메타데이터를 보존할 수 있다. 이러한 아티팩트(Artifact)는 실패를 재현 가능하게 만들고 회귀 분석(Regression Analysis)을 위한 증거를 제공한다. 실패한 CI 실행에는 엔지니어가 전체 시나리오를 대화형으로 다시 실행하지 않고도 영향을 받은 단계를 식별할 수 있을 만큼 충분한 정보가 포함되어야 한다.

종단 간 시나리오는 상당한 공유 상태(Shared State)를 포함하므로 테스트 격리(Test Isolation)가 필요하다. 임시 지도, 구성 파일, 데이터베이스, 캐시(Cache), 네임스페이스(Namespace), 포트(Port), 생성된 출력은 테스트 실행 사이에서 분리되어야 한다. 이전 시나리오에서 실행된 프로세스가 남아 후속 테스트 실행에 영향을 주어서는 안 된다. 따라서 신뢰할 수 있는 정리(Cleanup)는 성공적인 테스트 이후 선택적으로 수행하는 편의 기능이 아니라 프레임워크 자체의 일부이다.

통합 범위가 확대될수록 환경 재현성(Environment Reproducibility)은 더욱 중요해진다. 컨테이너 이미지(Container Image), 고정된 의존성(Pinned Dependency), 알려진 ROS 2 구성, 제어된 모델 아티팩트(Model Artifact), 버전이 관리되는 테스트 데이터셋을 사용하면 개발자 시스템과 CI 작업 환경 사이의 차이를 줄일 수 있다. 소프트웨어 리비전(Software Revision), 구성 리비전(Configuration Revision), 테스트 데이터 버전 및 관련 런타임 의존성(Runtime Dependency)은 필요할 때 과거의 실패를 다시 재현할 수 있도록 추적 가능해야 한다.

병렬 실행(Parallel Execution)은 테스트 시간을 단축할 수 있지만 리소스와 네임스페이스가 충분히 격리된 경우에만 시나리오를 병렬화해야 한다. 그렇지 않으면 여러 ROS 2 그래프가 디스커버리(Discovery), 공유 네트워크 리소스, 데이터베이스, GPU 할당 또는 고정된 장치 이름을 통해 서로 간섭할 수 있다. 특히 인지 모델이나 계산량이 많은 플래너(Planner)가 동일한 테스트 작업 환경의 가속기(Accelerator)와 메모리를 경쟁적으로 사용하는 경우 리소스 인식 스케줄링(Resource-Aware Scheduling)이 중요하다.

모든 시나리오를 벤치마크(Benchmark)로 전환하지 않으면서도 종단 간 실행 과정에서 성능 관측값(Performance Observation)을 수집할 수 있다. 프레임워크는 처리 지연시간(Processing Latency), 메시지 경과 시간(Message Age), 누락된 갱신, 계획 소요 시간, 리소스 사용량을 기록하고 이를 광범위한 회귀 임계값(Regression Threshold)과 비교할 수 있다. 엄격한 성능 인증은 별도의 활동으로 유지해야 하지만 큰 타이밍 변화는 기능적 합격 또는 불합격 검사만으로는 발견하기 어려운 통합 문제의 초기 증거를 제공할 수 있다.

프레임워크는 긍정 시나리오(Positive Scenario)와 부정 시나리오(Negative Scenario)를 모두 지원해야 한다. 긍정 테스트는 유효한 요청이 성공적으로 완료되는지를 검증하며, 부정 테스트는 잘못되거나 사용할 수 없거나 위험한 조건이 올바르게 거부되는지를 검증한다. 성숙한 테스트 스위트(Test Suite)는 정상적인 작업 흐름, 경계 사례(Boundary Case), 복구 경로(Recovery Path), 대표적인 실패 조건을 포함하여 소프트웨어 통합을 단순히 성공할 수 있는 능력뿐만 아니라 안전하게 실패할 수 있는 능력까지 평가한다.

지속적 통합(CI, Continuous Integration)에서는 더 빠른 단위 테스트와 집중된 통합 테스트가 통과한 이후 종단 간 테스트를 실행해야 한다. 이러한 순서는 이미 하위 수준 계약을 위반한 소프트웨어에 비용이 높은 리소스를 소비하는 것을 방지한다. 선택된 스모크 시나리오(Smoke Scenario)는 모든 변경사항에서 실행할 수 있으며, 보다 광범위한 회귀 테스트 스위트는 예약된 파이프라인이나 릴리스 중심 파이프라인에서 실행할 수 있다. 테스트 결과는 소프트웨어 리비전 전체에 걸쳐 실패를 추적할 수 있도록 기계 판독형(Machine-Readable)으로 유지해야 한다.

종단 간 소프트웨어 통합 테스트는 시뮬레이션(Simulation), 하드웨어 인더루프(HIL, Hardware-in-the-Loop), 현장 검증(Field Validation)을 대체하지 않는다. 제어된 소프트웨어 입력만으로는 물리적 동역학(Physical Dynamics), 센서 불확실성, 액추에이터 동작, 환경 변화(Environmental Variability), 실시간 하드웨어 상호작용을 완전히 재현할 수 없다. 대신 이 프레임워크는 통합된 소프트웨어 스택이 완전한 로봇 작업 흐름을 일관되게 실행할 수 있는지를 확인한 후 점차 현실성과 비용이 높아지는 검증 환경으로 진행할 수 있도록 한다.

잘 설계된 종단 간 프레임워크는 구성요소 수준의 정확성과 시스템 수준 소프트웨어 동작(System-Level Software Behavior)을 연결한다. 재현 가능한 시나리오, 제어된 입력, 실제 배포 환경과 유사한 ROS 2 구성, 중간 체크포인트, 결함 주입, 자동화된 증거 수집(Automated Evidence Collection), CI 실행을 결합함으로써 로봇 소프트웨어 스택이 하나의 조정된 시스템(Coordinated System)으로 동작하는지를 반복적으로 판단할 수 있는 방법을 제공하며, 이후 API, 데이터 파이프라인(Data Pipeline), HIL, 시뮬레이션 및 물리적 테스트 단계로 검증을 확장할 수 있는 기반을 제공한다.

##  

## 02.08. API Integration Test REST gRPC Robot [w/Code]

![](images/image8.png){width="7.268055555555556in" height="7.268055555555556in"}

Robot software increasingly exposes application programming interfaces that connect onboard autonomy, fleet management, cloud services, operator applications, databases, and external automation systems. API integration testing verifies that these interfaces exchange commands, state, telemetry, and results correctly across real software boundaries. Within the chapter structure, REST and gRPC testing extends integration verification beyond ROS 2 node graphs and end-to-end internal software workflows.

An API integration test should exercise the deployed interface rather than call the underlying business logic directly. The test client sends a request through the actual HTTP or gRPC endpoint, allowing serialization, transport, routing, authentication hooks, validation, service logic, and response generation to participate. This distinguishes API integration testing from unit tests that verify handler functions or message conversion utilities in isolation.

The test environment should reproduce the service topology required by the API while controlling dependencies that are outside the verification objective. A robot API service may communicate with mission management, telemetry storage, ROS 2 gateways, or fleet services. Required components can run as real integration targets, while unrelated cloud or hardware dependencies can be represented by controlled substitutes to keep execution deterministic and failures diagnosable.

REST API testing begins with verification of HTTP methods, resource paths, request headers, payload formats, and response status codes. Tests should confirm that valid GET, POST, PUT, PATCH, or DELETE operations behave according to the defined contract. Robot-specific resources may include missions, maps, robot state, configuration, charging requests, task assignments, diagnostics, or software-management operations depending on the platform architecture.

Request-schema validation should be exercised systematically. Tests can submit complete valid payloads, omit mandatory fields, provide unknown fields, use incorrect data types, or supply values outside allowed ranges. The API should reject invalid commands before they propagate into robot control logic. This is particularly important for parameters such as velocity limits, target poses, task identifiers, map references, or operational modes that can influence physical behavior.

Response validation should examine more than the HTTP status code. A successful response should contain the expected schema, field types, identifiers, timestamps, state values, and application-level result information. Error responses should also follow a predictable structure so clients can distinguish validation failures, unavailable resources, conflicting state, authorization problems, internal errors, and temporary service unavailability without parsing arbitrary text.

State-changing REST operations require careful integration testing because repeated requests may produce unintended robot actions. Where the API contract requires idempotency, tests should verify that retrying the same request does not create duplicate missions or repeated commands. Where operations are intentionally non-idempotent, the resulting state transitions should be explicit. This becomes important when clients automatically retry requests after communication interruptions.

gRPC integration testing focuses on the service and message contracts defined through Protocol Buffers. A test client can invoke the generated service stub using known request messages and inspect the returned response. The test should verify field semantics, enumeration values, nested messages, optional or required application-level information, and compatibility between the client and server implementations rather than merely confirming that the remote procedure call completed.

Unary gRPC calls can be tested similarly to conventional request-response operations, but streaming interfaces require additional scenarios. Server streaming may deliver continuous robot telemetry, client streaming may upload sequences of data, and bidirectional streaming may support interactive control or status exchange. Tests should verify stream establishment, message ordering where guaranteed, normal completion, cancellation, disconnection, and recovery behavior according to the service contract.

Deadlines and timeouts are essential for robot APIs because waiting indefinitely for a remote operation can block higher-level autonomy or operator workflows. Integration tests should configure realistic deadlines and deliberately delay or suppress responses to confirm that clients and servers handle expiration correctly. A timeout should result in a defined error path, diagnostic event, retry policy, or safe application state rather than an uncontrolled blocking condition.

API tests should verify error propagation across software layers. A REST endpoint may successfully receive a request while an internal ROS 2 service, database operation, or mission manager fails. Similarly, a gRPC server may accept a command but be unable to execute the requested robot operation. Integration testing should confirm that internal failures are translated into stable external error contracts without exposing implementation details or falsely reporting success.

Authentication and authorization behavior should be included when they are part of the deployed API contract. Tests can verify accepted credentials, missing credentials, expired or invalid credentials, and attempts to invoke operations without the required permission. Security testing is broader than functional API integration testing, but basic access-control behavior should still be verified because incorrect authorization can expose safety-relevant robot commands or sensitive operational data.

Concurrency scenarios are important when multiple clients can interact with the same robot or fleet service. Tests can issue simultaneous task requests, configuration updates, or state queries and observe whether shared resources remain consistent. Conflicting commands should be resolved according to a defined policy rather than producing race-dependent behavior. Transaction identifiers, revision numbers, locks, or explicit conflict responses can be validated where the architecture provides them.

Robot API integration tests should also examine the boundary between external interfaces and ROS 2. A REST mission request may be converted into a ROS 2 action goal, while telemetry from ROS 2 topics may be transformed into REST responses or gRPC streams. Tests should verify field mapping, units, coordinate frames, timestamps, identifiers, and state semantics across this gateway because translation errors can remain invisible when either side is tested independently.

Test data should include both nominal and boundary scenarios. A target pose may be valid, outside an allowed operating area, malformed, or associated with an unavailable map. A mission identifier may exist, be unknown, or refer to a completed operation. By controlling these conditions, the test suite verifies not only successful API communication but also the behavior of the integrated software when requests cannot legitimately be executed.

Service availability and reconnection should be tested where distributed robot software must tolerate temporary network failures. The test framework can terminate an API server, interrupt a dependent service, or force a connection to close and then restore it. Clients should respond according to their defined recovery strategy, avoiding uncontrolled request duplication, stale state, or indefinite blocking when communication becomes available again.

Version compatibility becomes important as robot and fleet software evolve independently. Integration tests can verify that supported API versions preserve required fields and semantics and that incompatible versions fail clearly. For Protocol Buffers, changes to field definitions should respect the intended compatibility strategy. REST APIs may use explicit versioned paths or schemas, and regression tests should protect externally consumed contracts during internal refactoring.

Observability should be incorporated into API testing so failures can be traced across distributed services. Request identifiers, timestamps, service logs, gRPC status information, HTTP responses, and relevant ROS 2 events can be collected with each scenario. Correlating these records helps determine whether a failure originated in transport, validation, gateway conversion, robot software, or a downstream service rather than simply reporting that the external request failed.

Continuous integration can execute API integration tests after unit and focused component tests succeed. The pipeline can start the required services, wait for readiness, execute REST and gRPC scenarios, collect results, and shut down the environment cleanly. Contract-focused smoke tests may run frequently, while larger failure, concurrency, compatibility, and recovery suites can execute in broader regression pipelines before release.

API integration testing therefore verifies the software boundary through which robot capabilities become accessible to other systems. By exercising actual REST and gRPC transports, validating schemas and state transitions, testing failures and timeouts, checking ROS 2 gateway mappings, and preserving reproducible evidence, the test framework establishes confidence that external clients can interact with robot software predictably before verification expands to data pipelines and complete deployment environments.

로봇 소프트웨어는 온보드 자율주행(Onboard Autonomy), 플릿 관리(Fleet Management), 클라우드 서비스(Cloud Service), 운영자 애플리케이션(Operator Application), 데이터베이스(Database), 외부 자동화 시스템(External Automation System)을 연결하는 응용 프로그래밍 인터페이스(API, Application Programming Interface)를 점점 더 광범위하게 제공하고 있다. API 통합 테스트(API Integration Testing)는 이러한 인터페이스가 실제 소프트웨어 경계를 넘어 명령, 상태, 텔레메트리(Telemetry), 실행 결과를 올바르게 교환하는지를 검증한다. 이 장의 구조에서 REST 및 gRPC 테스트는 ROS 2 노드 그래프와 종단 간 내부 소프트웨어 작업 흐름을 넘어 통합 검증 범위를 확장한다.

API 통합 테스트는 기반 비즈니스 로직(Business Logic)을 직접 호출하는 대신 실제 배포 인터페이스(Deployed Interface)를 통해 동작해야 한다. 테스트 클라이언트(Test Client)는 실제 HTTP 또는 gRPC 종단점(Endpoint)을 통해 요청을 전송하여 직렬화(Serialization), 전송(Transport), 라우팅(Routing), 인증 훅(Authentication Hook), 유효성 검증(Validation), 서비스 로직(Service Logic), 응답 생성(Response Generation)이 모두 테스트 과정에 참여하도록 한다. 이러한 특성은 핸들러 함수나 메시지 변환 유틸리티를 격리하여 검증하는 단위 테스트와 API 통합 테스트를 구분한다.

테스트 환경(Test Environment)은 검증 목적에 포함되지 않는 의존성을 제어하면서 API가 요구하는 서비스 토폴로지(Service Topology)를 재현해야 한다. 로봇 API 서비스는 임무 관리(Mission Management), 텔레메트리 저장소(Telemetry Storage), ROS 2 게이트웨이(Gateway), 플릿 서비스(Fleet Service)와 통신할 수 있다. 필요한 구성요소는 실제 통합 대상으로 실행하고, 관련성이 낮은 클라우드 또는 하드웨어 의존성은 제어 가능한 대체 요소로 구성하여 실행의 결정성(Determinism)을 유지하고 실패 원인을 쉽게 진단할 수 있도록 해야 한다.

REST API 테스트는 HTTP 메서드(Method), 리소스 경로(Resource Path), 요청 헤더(Request Header), 페이로드 형식(Payload Format), 응답 상태 코드(Response Status Code)를 검증하는 것에서 시작한다. 테스트에서는 유효한 GET, POST, PUT, PATCH, DELETE 작업이 정의된 계약에 따라 동작하는지 확인해야 한다. 로봇 플랫폼 아키텍처에 따라 로봇 전용 리소스에는 임무(Mission), 지도(Map), 로봇 상태(Robot State), 구성(Configuration), 충전 요청(Charging Request), 작업 할당(Task Assignment), 진단(Diagnostics), 소프트웨어 관리 작업 등이 포함될 수 있다.

요청 스키마 검증(Request-Schema Validation)은 체계적으로 수행해야 한다. 테스트에서는 완전하고 유효한 페이로드를 제출하는 것뿐만 아니라 필수 필드를 생략하거나, 알 수 없는 필드를 제공하거나, 잘못된 데이터 타입을 사용하거나, 허용 범위를 벗어난 값을 입력할 수 있다. API는 잘못된 명령이 로봇 제어 로직으로 전달되기 전에 이를 거부해야 한다. 특히 속도 제한, 목표 자세(Target Pose), 작업 식별자(Task Identifier), 지도 참조(Map Reference), 운용 모드(Operational Mode)와 같이 물리적 동작에 영향을 줄 수 있는 매개변수에서는 이러한 검증이 중요하다.

응답 검증(Response Validation)은 HTTP 상태 코드만 검사해서는 안 된다. 성공적인 응답에는 예상된 스키마, 필드 타입, 식별자, 타임스탬프(Timestamp), 상태값, 애플리케이션 수준 결과 정보(Application-Level Result Information)가 포함되어야 한다. 오류 응답 역시 예측 가능한 구조를 따라야 하며, 이를 통해 클라이언트가 임의의 텍스트를 분석하지 않고도 유효성 검증 실패, 사용할 수 없는 리소스, 상태 충돌, 권한 문제, 내부 오류, 일시적인 서비스 비가용성을 구분할 수 있어야 한다.

상태를 변경하는 REST 작업(State-Changing REST Operation)은 반복 요청이 의도하지 않은 로봇 동작을 발생시킬 수 있으므로 신중한 통합 테스트가 필요하다. API 계약에서 멱등성(Idempotency)을 요구하는 경우 동일한 요청을 재시도하더라도 중복 임무나 반복 명령이 생성되지 않는지 검증해야 한다. 작업이 의도적으로 비멱등적(Non-Idempotent)이라면 그에 따른 상태 전이가 명확해야 한다. 이는 통신 장애 이후 클라이언트가 요청을 자동으로 재시도하는 환경에서 특히 중요하다.

gRPC 통합 테스트는 프로토콜 버퍼(Protocol Buffers)를 통해 정의된 서비스 및 메시지 계약(Service and Message Contract)에 초점을 맞춘다. 테스트 클라이언트는 알려진 요청 메시지를 사용하여 생성된 서비스 스텁(Service Stub)을 호출하고 반환된 응답을 검사할 수 있다. 테스트에서는 원격 프로시저 호출(Remote Procedure Call)이 완료되었다는 사실만 확인하는 것이 아니라 필드 의미, 열거형 값(Enumeration Value), 중첩 메시지(Nested Message), 선택적 또는 애플리케이션 수준의 필수 정보, 클라이언트와 서버 구현 간 호환성을 검증해야 한다.

단항 gRPC 호출(Unary gRPC Call)은 일반적인 요청-응답 작업과 유사하게 테스트할 수 있지만 스트리밍 인터페이스(Streaming Interface)는 추가적인 시나리오를 요구한다. 서버 스트리밍(Server Streaming)은 연속적인 로봇 텔레메트리를 전달할 수 있고, 클라이언트 스트리밍(Client Streaming)은 데이터 시퀀스를 업로드할 수 있으며, 양방향 스트리밍(Bidirectional Streaming)은 대화형 제어 또는 상태 교환을 지원할 수 있다. 테스트에서는 서비스 계약에 따라 스트림 연결, 보장되는 경우의 메시지 순서, 정상 종료, 취소, 연결 해제, 복구 동작을 검증해야 한다.

데드라인(Deadline)과 타임아웃(Timeout)은 원격 작업을 무한정 기다릴 경우 상위 수준 자율 기능이나 운영자 작업 흐름을 차단할 수 있으므로 로봇 API에서 필수적인 요소이다. 통합 테스트에서는 현실적인 데드라인을 설정하고 의도적으로 응답을 지연시키거나 억제하여 클라이언트와 서버가 만료 상황을 올바르게 처리하는지 확인해야 한다. 타임아웃은 제어되지 않은 블로킹 상태가 아니라 정의된 오류 경로(Error Path), 진단 이벤트(Diagnostic Event), 재시도 정책(Retry Policy), 안전한 애플리케이션 상태로 이어져야 한다.

API 테스트는 소프트웨어 계층 간 오류 전파(Error Propagation)를 검증해야 한다. REST 종단점이 요청을 정상적으로 수신했더라도 내부 ROS 2 서비스, 데이터베이스 작업 또는 임무 관리자가 실패할 수 있다. 마찬가지로 gRPC 서버가 명령을 수신했지만 요청된 로봇 작업을 실행할 수 없는 상황도 발생할 수 있다. 통합 테스트에서는 내부 실패가 구현 세부사항을 노출하거나 잘못된 성공을 보고하지 않으면서 안정적인 외부 오류 계약(External Error Contract)으로 변환되는지 확인해야 한다.

인증(Authentication) 및 권한 부여(Authorization)가 실제 배포 API 계약의 일부라면 해당 동작도 테스트에 포함해야 한다. 테스트에서는 허용된 자격 증명(Credential), 누락된 자격 증명, 만료되거나 잘못된 자격 증명, 필요한 권한 없이 작업을 호출하려는 시도를 검증할 수 있다. 보안 테스트(Security Testing)는 기능적 API 통합 테스트보다 광범위하지만, 잘못된 권한 제어는 안전과 관련된 로봇 명령이나 민감한 운용 데이터를 노출할 수 있으므로 기본적인 접근 제어(Access Control) 동작은 반드시 검증해야 한다.

여러 클라이언트가 동일한 로봇 또는 플릿 서비스와 상호작용할 수 있는 경우 동시성 시나리오(Concurrency Scenario)가 중요하다. 테스트에서는 여러 작업 요청, 구성 갱신 또는 상태 질의를 동시에 실행하고 공유 리소스(Shared Resource)가 일관성을 유지하는지 관찰할 수 있다. 충돌하는 명령은 경쟁 상태(Race Condition)에 따라 임의로 처리되는 대신 정의된 정책에 따라 해결되어야 한다. 아키텍처에서 제공하는 경우 트랜잭션 식별자(Transaction Identifier), 리비전 번호(Revision Number), 잠금(Lock), 명시적인 충돌 응답을 검증할 수 있다.

로봇 API 통합 테스트에서는 외부 인터페이스와 ROS 2 사이의 경계도 검사해야 한다. REST 임무 요청은 ROS 2 액션 목표(Action Goal)로 변환될 수 있으며, ROS 2 토픽의 텔레메트리는 REST 응답이나 gRPC 스트림으로 변환될 수 있다. 테스트에서는 이 게이트웨이를 통과하는 필드 매핑(Field Mapping), 단위(Unit), 좌표 프레임(Coordinate Frame), 타임스탬프, 식별자, 상태 의미론(State Semantics)을 검증해야 한다. 양쪽을 독립적으로 테스트할 경우 이러한 변환 오류가 발견되지 않을 수 있기 때문이다.

테스트 데이터(Test Data)는 정상 시나리오와 경계 시나리오(Boundary Scenario)를 모두 포함해야 한다. 목표 자세는 유효하거나, 허용된 운용 영역 밖에 있거나, 잘못 구성되거나, 사용할 수 없는 지도와 연결될 수 있다. 임무 식별자는 존재하거나, 알 수 없거나, 이미 완료된 작업을 참조할 수 있다. 이러한 조건을 제어함으로써 테스트 스위트(Test Suite)는 성공적인 API 통신뿐만 아니라 요청을 정상적으로 실행할 수 없는 상황에서 통합 소프트웨어가 어떻게 동작하는지도 검증할 수 있다.

분산 로봇 소프트웨어(Distributed Robot Software)가 일시적인 네트워크 장애를 허용해야 하는 경우 서비스 가용성(Service Availability)과 재연결(Reconnection)도 테스트해야 한다. 테스트 프레임워크는 API 서버를 종료하거나, 종속 서비스를 중단하거나, 연결을 강제로 종료한 후 다시 복구할 수 있다. 클라이언트는 정의된 복구 전략(Recovery Strategy)에 따라 대응해야 하며, 통신이 복구된 이후 제어되지 않은 요청 중복, 오래된 상태(Stale State), 무기한 블로킹이 발생해서는 안 된다.

로봇 및 플릿 소프트웨어가 서로 독립적으로 발전할수록 버전 호환성(Version Compatibility)이 중요해진다. 통합 테스트에서는 지원되는 API 버전이 필요한 필드와 의미론을 유지하는지, 호환되지 않는 버전은 명확하게 실패하는지 검증할 수 있다. 프로토콜 버퍼의 경우 필드 정의 변경은 의도된 호환성 전략(Compatibility Strategy)을 따라야 한다. REST API는 명시적으로 버전이 지정된 경로나 스키마를 사용할 수 있으며, 회귀 테스트는 내부 리팩터링 과정에서도 외부에서 사용하는 계약을 보호해야 한다.

분산 서비스 전체에서 실패를 추적할 수 있도록 관측 가능성(Observability)을 API 테스트에 포함해야 한다. 각 시나리오에서 요청 식별자(Request Identifier), 타임스탬프, 서비스 로그(Service Log), gRPC 상태 정보, HTTP 응답, 관련 ROS 2 이벤트를 수집할 수 있다. 이러한 기록을 상호 연계하면 단순히 외부 요청이 실패했다는 결과만 제공하는 대신 전송, 유효성 검증, 게이트웨이 변환, 로봇 소프트웨어 또는 하위 서비스 중 어디에서 실패가 발생했는지 파악할 수 있다.

지속적 통합(CI, Continuous Integration)은 단위 테스트와 집중된 구성요소 테스트가 성공한 이후 API 통합 테스트를 실행할 수 있다. 파이프라인은 필요한 서비스를 시작하고, 준비 완료를 기다린 후, REST 및 gRPC 시나리오를 실행하고, 결과를 수집하며, 테스트 환경을 정상적으로 종료할 수 있다. 계약 중심의 스모크 테스트(Contract-Focused Smoke Test)는 자주 실행하고, 보다 광범위한 실패, 동시성, 호환성, 복구 테스트 스위트는 릴리스 이전의 전체 회귀 파이프라인에서 실행할 수 있다.

API 통합 테스트는 로봇의 기능이 다른 시스템에서 접근 가능해지는 소프트웨어 경계를 검증한다. 실제 REST 및 gRPC 전송을 실행하고, 스키마와 상태 전이를 검증하며, 실패와 타임아웃을 테스트하고, ROS 2 게이트웨이 매핑을 확인하며, 재현 가능한 검증 증거를 보존함으로써 외부 클라이언트가 로봇 소프트웨어와 예측 가능한 방식으로 상호작용할 수 있다는 신뢰성을 확보한다. 이를 기반으로 이후 데이터 파이프라인(Data Pipeline) 및 완전한 배포 환경(Complete Deployment Environment)으로 검증 범위를 확장할 수 있다.

##  

## 02.09. Database and Data Pipeline Integration Test [w/Code]

![](images/image9.png){width="7.268055555555556in" height="7.268055555555556in"}

Database and data-pipeline integration testing verifies that robot software can persist, retrieve, transform, transport, and consume operational data correctly across service boundaries. Modern robots generate mission records, maps, telemetry, diagnostics, perception results, configuration histories, and maintenance information. Testing these paths ensures that valid information remains consistent from the robot software that produces it to the applications and services that later consume it.

The integration boundary should include the real database interface and the important stages of the data pipeline rather than replacing every dependency with an in-memory mock. A controlled test environment can instantiate the database, schema, message broker, storage service, or processing component required by the architecture. External systems outside the verification objective may still be substituted so that failures remain reproducible and attributable to the tested pipeline.

Database schema initialization is a fundamental test target. A fresh environment should create the required tables, collections, indexes, constraints, and metadata without manual intervention. Tests should also confirm that application services can start against the initialized schema and that expected fields use compatible types and constraints. Missing indexes or incorrect relationships may not cause immediate functional failure but can reveal deployment inconsistencies.

Create, read, update, and delete operations should be verified through the same repository or service interfaces used by production robot software. A mission record written by one component should be retrievable by another with equivalent identifiers, timestamps, state fields, and associated metadata. Updates should modify only intended fields, while deletion or archival behavior should preserve referential and operational rules defined by the system.

Transaction behavior becomes important when a robot operation modifies several related records. Assigning a mission may update the mission state, robot allocation, event history, and scheduling information as one logical operation. Integration tests should deliberately cause failure during intermediate steps and verify that the database preserves the intended atomicity. Partially committed state can otherwise leave fleet software with contradictory information about robot availability or task ownership.

Data integrity constraints should be exercised with both valid and invalid records. Tests can attempt to insert duplicate identifiers, missing required fields, invalid references, malformed timestamps, or values outside application-defined ranges. The database and application layer should reject inconsistent information according to their respective responsibilities. Error handling should remain predictable so upstream services can distinguish validation failures from infrastructure failures.

Robot timestamps deserve particular attention because data may originate from multiple computers, sensors, and cloud services. Integration tests should verify timestamp representation, timezone handling, precision, ordering, and conversion across storage boundaries. Telemetry or event pipelines should preserve the temporal relationships needed for diagnostics and replay. Incorrect conversions can make valid robot events appear out of order even when every individual message is otherwise correct.

Data serialization and deserialization should preserve the semantic content of robot information. ROS 2 messages, JSON documents, Protocol Buffer messages, binary sensor records, or custom structures may be transformed before storage or transmission. Tests should verify field mapping, units, coordinate-frame identifiers, enumeration values, optional fields, and numerical precision so information does not silently change meaning while crossing representation boundaries.

A data pipeline often contains producers, brokers, processors, storage systems, and downstream consumers. Integration testing should follow representative records through these stages and confirm that each expected transformation occurs. For example, robot telemetry may be published by an onboard service, normalized by a gateway, transferred through a message system, stored in a time-series database, and later retrieved by a monitoring application.

Ordering behavior should be tested when downstream logic depends on event sequence. Distributed systems can introduce delayed, duplicated, or reordered messages even when individual producers behave correctly. The pipeline should define how sequence numbers, timestamps, partitioning, or application logic preserve required ordering. Tests can intentionally alter arrival order and verify that consumers either reconstruct the intended sequence or handle unordered information safely.

Duplicate delivery is another important integration condition because many messaging systems provide at-least-once delivery semantics. A test can deliver the same telemetry record, mission event, or processing request multiple times and observe whether duplicate storage or repeated side effects occur. Where idempotent processing is required, stable event identifiers or deduplication logic should ensure that retries do not corrupt accumulated robot state.

Missing or delayed data should produce defined behavior. A telemetry pipeline may temporarily lose network connectivity, a database may become unavailable, or a processing service may stop consuming messages. Tests should verify buffering, retry, backpressure, expiration, or failure-reporting policies according to the architecture. Recovery should not silently discard critical records or overwhelm downstream services with uncontrolled retransmission.

Pipeline transformation logic should be tested with known input and expected output datasets. Raw robot observations may be filtered, aggregated, enriched with metadata, converted into engineering units, or summarized into operational metrics. Deterministic fixtures allow the transformed records to be compared field by field with expected values. This separates transformation correctness from broader analytics or machine-learning quality evaluation.

Large binary artifacts require additional integration checks when the robot stores maps, images, point clouds, logs, or AI-related datasets outside the primary database. Metadata records should reference the correct object, version, checksum, location, and ownership information. Tests should verify that an artifact written through the storage interface can later be retrieved and associated with the correct robot, mission, timestamp, or dataset without ambiguity.

Schema migration testing protects systems that evolve while retaining historical robot data. A test environment can begin with an earlier supported schema, populate representative records, execute the migration, and verify that the updated application can read and modify the migrated data. Migration tests should detect lost fields, incorrect defaults, incompatible type conversions, or changes that break services still expecting a supported historical representation.

Concurrent access should be evaluated when multiple robot or fleet services read and update shared information. Tests can simulate simultaneous mission assignment, robot-state updates, configuration changes, or telemetry writes. The resulting records should satisfy the defined consistency model. Lost updates, conflicting ownership, or race-dependent state transitions should be detected before deployment where concurrency is significantly harder to reproduce.

Failure injection should include database disconnection, broker interruption, malformed records, processing exceptions, and temporary downstream unavailability. The objective is to verify the behavior of the integrated pipeline rather than merely confirm that an exception occurs. Components should preserve recoverable data, report meaningful diagnostics, avoid uncontrolled retry loops, and resume processing according to the defined recovery strategy when dependencies return.

Observability is essential because a pipeline failure may occur several services away from the original robot event. Integration tests should capture correlation identifiers, processing timestamps, queue state, database errors, transformation logs, retry counts, and relevant service diagnostics. These records make it possible to determine where a message was delayed, rejected, duplicated, transformed incorrectly, or lost during a regression test.

Test isolation should prevent one execution from contaminating another. Each scenario can use a dedicated database, schema, namespace, topic, bucket, or temporary storage location depending on the technology. Test data should be created automatically and removed or reset after execution. Reliable isolation enables parallel CI runs and prevents old robot records from producing false positives or hiding failures in later scenarios.

Continuous integration can execute focused database and pipeline tests after unit, node-graph, end-to-end, and API contract checks have established earlier software correctness. The pipeline can provision temporary infrastructure, apply schemas, load deterministic fixtures, execute data flows, inspect stored results, and destroy the environment. More expensive migration, recovery, concurrency, and volume-oriented scenarios can run in scheduled regression pipelines.

Database and data-pipeline integration testing therefore establishes confidence that robot information remains usable beyond the process that originally created it. By verifying persistence, transactions, schemas, serialization, ordering, duplicate handling, transformations, migrations, recovery, and observability, the test framework protects the continuity of operational data across the robot software ecosystem and prepares the integrated stack for subsequent performance and reliability testing.

데이터베이스 및 데이터 파이프라인 통합 테스트(Database and Data-Pipeline Integration Testing)는 로봇 소프트웨어가 서비스 경계(Service Boundary)를 넘어 운용 데이터를 올바르게 영속화(Persist), 검색(Retrieve), 변환(Transform), 전송(Transport), 소비(Consume)할 수 있는지를 검증한다. 현대 로봇은 임무 기록(Mission Record), 지도(Map), 텔레메트리(Telemetry), 진단 정보(Diagnostics), 인지 결과(Perception Result), 구성 이력(Configuration History), 유지보수 정보(Maintenance Information)를 생성한다. 이러한 경로를 테스트하면 데이터를 생성한 로봇 소프트웨어에서 이후 이를 사용하는 애플리케이션과 서비스에 이르기까지 유효한 정보의 일관성을 유지할 수 있다.

통합 경계(Integration Boundary)는 모든 의존성을 인메모리 모의 객체(In-Memory Mock)로 대체하는 대신 실제 데이터베이스 인터페이스와 데이터 파이프라인(Data Pipeline)의 주요 단계를 포함해야 한다. 제어된 테스트 환경에서는 아키텍처에서 요구하는 데이터베이스, 스키마(Schema), 메시지 브로커(Message Broker), 스토리지 서비스(Storage Service), 처리 구성요소(Processing Component)를 구성할 수 있다. 검증 목적에 포함되지 않는 외부 시스템은 대체 요소로 구성하여 실패를 재현 가능하게 유지하고 테스트 대상 파이프라인에서 실패 원인을 명확하게 식별할 수 있도록 한다.

데이터베이스 스키마 초기화(Database Schema Initialization)는 기본적인 테스트 대상이다. 새로운 환경에서는 필요한 테이블(Table), 컬렉션(Collection), 인덱스(Index), 제약조건(Constraint), 메타데이터(Metadata)를 수동 개입 없이 생성할 수 있어야 한다. 또한 애플리케이션 서비스가 초기화된 스키마를 기반으로 정상적으로 시작할 수 있는지, 예상되는 필드가 호환 가능한 데이터 타입과 제약조건을 사용하는지 확인해야 한다. 누락된 인덱스나 잘못된 관계는 즉각적인 기능 실패를 일으키지 않더라도 배포 환경의 불일치를 드러낼 수 있다.

생성, 읽기, 갱신, 삭제(CRUD, Create, Read, Update, Delete) 작업은 실제 운용 로봇 소프트웨어에서 사용하는 것과 동일한 저장소(Repository) 또는 서비스 인터페이스를 통해 검증해야 한다. 한 구성요소가 기록한 임무 레코드는 다른 구성요소에서 동일한 식별자, 타임스탬프(Timestamp), 상태 필드, 관련 메타데이터와 함께 검색할 수 있어야 한다. 갱신 작업은 의도한 필드만 수정해야 하며, 삭제 또는 보관(Archival) 동작은 시스템에서 정의한 참조 및 운용 규칙을 유지해야 한다.

하나의 로봇 작업이 서로 연관된 여러 레코드를 수정하는 경우 트랜잭션 동작(Transaction Behavior)이 중요해진다. 임무를 할당할 때 임무 상태, 로봇 할당 정보, 이벤트 이력(Event History), 스케줄링 정보를 하나의 논리적 작업으로 갱신할 수 있다. 통합 테스트에서는 중간 단계에서 의도적으로 실패를 발생시키고 데이터베이스가 정의된 원자성(Atomicity)을 유지하는지 검증해야 한다. 일부 상태만 커밋(Commit)되면 플릿 소프트웨어(Fleet Software)가 로봇 가용성이나 작업 소유권에 대해 서로 모순되는 정보를 갖게 될 수 있다.

데이터 무결성 제약조건(Data Integrity Constraint)은 유효한 레코드와 잘못된 레코드를 모두 사용하여 검증해야 한다. 테스트에서는 중복된 식별자, 누락된 필수 필드, 잘못된 참조, 비정상적인 타임스탬프, 애플리케이션에서 정의한 범위를 벗어난 값을 삽입할 수 있다. 데이터베이스와 애플리케이션 계층(Application Layer)은 각각의 책임에 따라 일관되지 않은 정보를 거부해야 한다. 오류 처리는 예측 가능한 방식으로 유지되어 상위 서비스가 유효성 검증 실패와 인프라 실패(Infrastructure Failure)를 구분할 수 있어야 한다.

로봇 데이터는 여러 컴퓨터, 센서, 클라우드 서비스에서 생성될 수 있으므로 로봇 타임스탬프(Robot Timestamp)는 특별한 주의가 필요하다. 통합 테스트에서는 스토리지 경계를 통과하는 과정에서 타임스탬프 표현, 시간대(Timezone) 처리, 정밀도(Precision), 순서(Ordering), 변환(Conversion)을 검증해야 한다. 텔레메트리 또는 이벤트 파이프라인은 진단과 재생(Replay)에 필요한 시간적 관계(Temporal Relationship)를 유지해야 한다. 잘못된 변환이 발생하면 개별 메시지가 모두 올바르더라도 정상적인 로봇 이벤트가 잘못된 순서로 발생한 것처럼 보일 수 있다.

데이터 직렬화 및 역직렬화(Serialization and Deserialization)는 로봇 정보의 의미적 내용(Semantic Content)을 보존해야 한다. ROS 2 메시지, JSON 문서, 프로토콜 버퍼(Protocol Buffer) 메시지, 바이너리 센서 레코드(Binary Sensor Record), 사용자 정의 구조(Custom Structure)는 저장 또는 전송 전에 다른 형식으로 변환될 수 있다. 테스트에서는 표현 형식의 경계를 통과하면서 정보의 의미가 조용히 변경되지 않도록 필드 매핑(Field Mapping), 단위(Unit), 좌표 프레임 식별자(Coordinate-Frame Identifier), 열거형 값(Enumeration Value), 선택적 필드(Optional Field), 수치 정밀도(Numerical Precision)를 검증해야 한다.

데이터 파이프라인은 일반적으로 생산자(Producer), 브로커(Broker), 처리기(Processor), 스토리지 시스템(Storage System), 하위 소비자(Downstream Consumer)로 구성된다. 통합 테스트에서는 대표적인 레코드가 이러한 단계를 통과하는 과정을 추적하고 각 단계에서 예상된 변환이 수행되는지 확인해야 한다. 예를 들어 로봇 텔레메트리는 온보드 서비스(Onboard Service)에서 발행되고, 게이트웨이(Gateway)에서 정규화된 후 메시지 시스템을 통해 전송되고, 시계열 데이터베이스(Time-Series Database)에 저장된 다음 모니터링 애플리케이션에서 다시 검색될 수 있다.

하위 로직이 이벤트 순서에 의존하는 경우 순서 처리 동작(Ordering Behavior)을 테스트해야 한다. 분산 시스템(Distributed System)에서는 개별 생산자가 올바르게 동작하더라도 메시지가 지연되거나, 중복되거나, 순서가 변경될 수 있다. 파이프라인에서는 시퀀스 번호(Sequence Number), 타임스탬프, 파티셔닝(Partitioning), 애플리케이션 로직을 이용하여 필요한 순서를 어떻게 유지할 것인지 정의해야 한다. 테스트에서는 의도적으로 도착 순서를 변경하고 소비자가 원래 순서를 복원하거나 순서가 뒤섞인 정보를 안전하게 처리하는지 검증할 수 있다.

많은 메시징 시스템이 최소 한 번 전달(At-Least-Once Delivery) 의미론을 제공하므로 중복 전달(Duplicate Delivery)도 중요한 통합 조건이다. 테스트에서는 동일한 텔레메트리 레코드, 임무 이벤트 또는 처리 요청을 여러 번 전달하고 중복 저장이나 반복적인 부수 효과(Side Effect)가 발생하는지 관찰할 수 있다. 멱등 처리(Idempotent Processing)가 필요한 경우 안정적인 이벤트 식별자(Event Identifier) 또는 중복 제거 로직(Deduplication Logic)을 통해 재시도가 누적된 로봇 상태를 손상시키지 않도록 해야 한다.

누락되거나 지연된 데이터(Missing or Delayed Data)는 정의된 동작을 발생시켜야 한다. 텔레메트리 파이프라인에서 일시적으로 네트워크 연결이 끊기거나, 데이터베이스를 사용할 수 없게 되거나, 처리 서비스가 메시지 소비를 중단할 수 있다. 테스트에서는 아키텍처에 따라 버퍼링(Buffering), 재시도(Retry), 백프레셔(Backpressure), 만료(Expiration), 실패 보고(Failure Reporting) 정책을 검증해야 한다. 복구 과정에서 중요한 레코드가 아무런 경고 없이 손실되거나 제어되지 않은 재전송으로 하위 서비스에 과도한 부하가 발생해서는 안 된다.

파이프라인 변환 로직(Pipeline Transformation Logic)은 알려진 입력과 예상 출력 데이터셋을 사용하여 테스트해야 한다. 원시 로봇 관측값(Raw Robot Observation)은 필터링되거나, 집계(Aggregation)되거나, 메타데이터가 추가되거나, 공학 단위(Engineering Unit)로 변환되거나, 운용 지표(Operational Metric)로 요약될 수 있다. 결정론적인 픽스처(Deterministic Fixture)를 사용하면 변환된 레코드를 예상값과 필드별로 비교할 수 있다. 이를 통해 변환 정확성을 보다 광범위한 분석 또는 머신러닝 품질 평가와 분리할 수 있다.

로봇이 지도, 이미지, 포인트 클라우드(Point Cloud), 로그(Log), AI 관련 데이터셋과 같은 대용량 바이너리 아티팩트(Binary Artifact)를 기본 데이터베이스 외부에 저장하는 경우 추가적인 통합 검사가 필요하다. 메타데이터 레코드는 올바른 객체, 버전, 체크섬(Checksum), 저장 위치, 소유권 정보를 참조해야 한다. 테스트에서는 스토리지 인터페이스를 통해 기록된 아티팩트를 이후 다시 검색하고 해당 로봇, 임무, 타임스탬프 또는 데이터셋과 모호함 없이 연결할 수 있는지 검증해야 한다.

스키마 마이그레이션 테스트(Schema Migration Testing)는 과거 로봇 데이터를 유지하면서 시스템이 발전하는 환경을 보호한다. 테스트 환경은 이전에 지원되던 스키마에서 시작하여 대표적인 레코드를 생성하고, 마이그레이션(Migration)을 실행한 다음, 갱신된 애플리케이션이 변환된 데이터를 읽고 수정할 수 있는지 검증할 수 있다. 마이그레이션 테스트에서는 필드 손실, 잘못된 기본값(Default Value), 호환되지 않는 데이터 타입 변환 또는 지원되는 과거 표현을 여전히 요구하는 서비스의 동작을 손상시키는 변경을 탐지해야 한다.

여러 로봇 또는 플릿 서비스가 공유 정보를 읽고 갱신하는 경우 동시 접근(Concurrent Access)을 평가해야 한다. 테스트에서는 임무 할당, 로봇 상태 갱신, 구성 변경 또는 텔레메트리 기록을 동시에 수행하도록 시뮬레이션할 수 있다. 결과 레코드는 정의된 일관성 모델(Consistency Model)을 만족해야 한다. 갱신 손실(Lost Update), 충돌하는 소유권 또는 경쟁 상태에 따라 달라지는 상태 전이(Race-Dependent State Transition)는 실제 배포 전에 탐지해야 한다. 실제 환경에서는 이러한 동시성 문제를 재현하기가 훨씬 어렵기 때문이다.

결함 주입(Failure Injection)은 데이터베이스 연결 해제, 브로커 중단, 잘못 구성된 레코드, 처리 예외(Processing Exception), 일시적인 하위 서비스 비가용성을 포함해야 한다. 목적은 단순히 예외가 발생하는지를 확인하는 것이 아니라 통합된 파이프라인의 동작을 검증하는 것이다. 구성요소는 복구 가능한 데이터를 보존하고, 의미 있는 진단 정보를 보고하며, 제어되지 않은 재시도 루프를 방지하고, 의존성이 복구되었을 때 정의된 복구 전략(Recovery Strategy)에 따라 처리를 다시 시작해야 한다.

파이프라인 실패는 원래 로봇 이벤트가 발생한 지점에서 여러 서비스 떨어진 위치에서 발생할 수 있으므로 관측 가능성(Observability)이 필수적이다. 통합 테스트에서는 상관 식별자(Correlation Identifier), 처리 타임스탬프(Processing Timestamp), 큐 상태(Queue State), 데이터베이스 오류, 변환 로그(Transformation Log), 재시도 횟수, 관련 서비스 진단 정보를 수집해야 한다. 이러한 기록을 통해 회귀 테스트 과정에서 메시지가 어디에서 지연, 거부, 중복, 잘못 변환 또는 손실되었는지를 판단할 수 있다.

테스트 격리(Test Isolation)는 하나의 실행 결과가 다른 실행을 오염시키는 것을 방지해야 한다. 기술에 따라 각 시나리오에서 전용 데이터베이스, 스키마, 네임스페이스(Namespace), 토픽(Topic), 버킷(Bucket), 임시 스토리지 위치를 사용할 수 있다. 테스트 데이터는 자동으로 생성되고 실행 이후 삭제되거나 초기화되어야 한다. 신뢰할 수 있는 격리는 병렬 지속적 통합(CI, Continuous Integration) 실행을 가능하게 하며 이전 로봇 레코드가 후속 시나리오에서 거짓 양성(False Positive)을 발생시키거나 실패를 숨기는 것을 방지한다.

지속적 통합(CI)은 단위 테스트, 노드 그래프 테스트, 종단 간 테스트, API 계약 검사(API Contract Check)를 통해 앞선 단계의 소프트웨어 정확성이 확보된 이후 집중적인 데이터베이스 및 파이프라인 테스트를 실행할 수 있다. 파이프라인은 임시 인프라를 구성하고, 스키마를 적용하며, 결정론적인 픽스처를 로딩하고, 데이터 흐름을 실행하며, 저장된 결과를 검사한 후 테스트 환경을 제거할 수 있다. 비용이 높은 마이그레이션, 복구, 동시성 및 데이터 볼륨 중심 시나리오는 예약된 회귀 파이프라인에서 실행할 수 있다.

데이터베이스 및 데이터 파이프라인 통합 테스트는 로봇 정보가 처음 생성된 프로세스를 벗어난 이후에도 계속 사용할 수 있다는 신뢰성을 확보한다. 영속성(Persistence), 트랜잭션(Transaction), 스키마, 직렬화, 순서 처리, 중복 처리, 변환, 마이그레이션, 복구, 관측 가능성을 검증함으로써 테스트 프레임워크는 로봇 소프트웨어 생태계 전체에서 운용 데이터의 연속성(Continuity)을 보호하고 통합된 소프트웨어 스택이 이후 성능 및 신뢰성 테스트(Performance and Reliability Testing) 단계로 진행할 수 있는 기반을 제공한다.

##  

## 02.10. CI Integrated Unit and Integration Test Pipeline [w/Code]

![](images/image10.png){width="7.268055555555556in" height="7.268055555555556in"}

A continuous integration pipeline for robot software combines unit and integration testing into an automated verification sequence that executes whenever software changes. Its purpose is to detect defects before they propagate into simulation, HIL, or physical robot testing. The pipeline connects source-code changes with reproducible builds, deterministic tests, evidence collection, and acceptance gates so software quality is evaluated continuously rather than only before release.

The pipeline should organize tests according to verification scope and execution cost. Fast unit tests normally run first because they isolate algorithms, utilities, controllers, perception inference wrappers, and other software components without requiring distributed services. More expensive ROS 2 integration, end-to-end, API, and data-pipeline tests follow only after the fundamental software checks succeed, reducing wasted compute resources and shortening feedback time for developers.

A CI run begins from a defined source revision and a reproducible build environment. Compiler versions, ROS 2 dependencies, middleware configuration, Python packages, inference runtimes, and external libraries should be controlled through versioned configuration or container images where practical. The pipeline should record the exact software revision and relevant environment information so a failed test can later be reproduced under equivalent conditions.

The build stage should verify that packages compile cleanly before functional tests begin. ROS 2 workspaces can be built with the required package dependencies and test options enabled, while compiler warnings and static-analysis findings may be collected according to project policy. A build failure should terminate dependent stages because integration results are not meaningful when the tested software artifact cannot be produced consistently.

Unit tests form the first executable verification gate. C++ tests based on GoogleTest or similar frameworks and Python tests based on PyTest can validate mathematical functions, state machines, controller algorithms, message-processing logic, inference preprocessing, and failure handling. These tests should remain deterministic and independent of unnecessary middleware, network, database, or physical hardware dependencies so they can execute rapidly on every relevant change.

ROS 2 package tests should integrate naturally with the workspace build and test system. Tests registered through ament can be executed as part of the automated pipeline, with results collected in a machine-readable form. Failed assertions, process errors, and package-level test results should be preserved as artifacts. This provides immediate traceability from a CI failure to the package and test case responsible for the regression.

After unit verification succeeds, focused ROS 2 node-graph integration tests can validate communication between production components. The pipeline may launch selected publishers, subscribers, services, actions, lifecycle nodes, and supporting processes using controlled configurations. Tests should wait for observable readiness conditions instead of arbitrary delays and then verify message exchange, QoS compatibility, state transitions, transforms, and defined failure behavior.

End-to-end software scenarios extend the pipeline across complete functional paths. A controlled navigation, manipulation, perception, or mission workflow can inject known inputs and observe intermediate checkpoints and final outputs. These scenarios should use production-like software composition while replacing physical hardware with deterministic sources where appropriate. The objective is to verify coordinated software behavior before introducing simulation or real-world uncertainty.

API integration stages can verify REST and gRPC boundaries used by fleet systems, operator applications, cloud services, or external automation. The CI environment can start the required API services, issue controlled requests, validate schemas and responses, exercise timeout and error paths, and confirm mappings into internal ROS 2 operations. Contract failures should be detected before incompatible software revisions are deployed together.

Database and data-pipeline tests can provision temporary infrastructure for persistence and information-flow verification. The pipeline may initialize schemas, load deterministic fixtures, execute representative telemetry or mission-data flows, and inspect stored or transformed results. Transaction behavior, serialization, duplicate handling, ordering, migration, and recovery scenarios can be included according to execution cost and the risk associated with the modified components.

Test environments should be isolated from one another to prevent state leakage. ROS 2 namespaces, databases, temporary files, network ports, caches, message queues, and generated artifacts should be separated when tests run concurrently or sequentially on shared workers. Cleanup must execute reliably even after failure so a crashed scenario does not leave processes or data that alter the outcome of subsequent CI jobs.

Parallelization can reduce total verification time when tests are independent and infrastructure resources permit it. Unit-test packages can often execute concurrently, while integration scenarios may require more careful scheduling because they compete for CPU, memory, network resources, databases, or GPUs. Resource-aware execution prevents unrelated tests from producing timing failures merely because several computationally intensive robotics workloads were scheduled on the same worker.

Flaky tests should be treated as engineering defects rather than hidden through unlimited retries. A test that intermittently fails because of arbitrary sleeps, uncontrolled timing, shared state, random seeds, or discovery races weakens confidence in the complete pipeline. CI infrastructure should preserve enough evidence to distinguish product failures from test-environment instability, while retries, if permitted, should remain bounded and visible in the reported result.

Failure diagnostics should be collected automatically at every significant stage. Useful evidence can include test reports, process logs, ROS 2 diagnostics, message traces, parameter snapshots, database errors, API responses, timestamps, core dumps, and relevant runtime metadata. Artifacts should be associated with the source revision and test scenario so engineers can investigate a regression without first attempting to reproduce an incompletely documented CI environment.

Coverage information can supplement test results by identifying software paths that are exercised or left untested. Line, branch, or function coverage may help reveal important gaps, but coverage percentage should not be treated as proof of behavioral correctness. Safety-relevant error handling, boundary conditions, state transitions, and interface contracts require explicit test scenarios even when overall numerical coverage appears high.

Pipeline gates should reflect the criticality and maturity of the robot software. A pull request may require successful compilation and all fast unit tests, while merging into a protected branch can additionally require ROS 2 integration and selected end-to-end scenarios. Release candidates can trigger broader API, database, recovery, compatibility, and regression suites. This layered policy balances rapid developer feedback with increasingly comprehensive verification.

Change-aware test selection can improve efficiency when the software repository becomes large. Modifications to a controller library may immediately trigger its unit tests and dependent ROS 2 integration scenarios, while changes to shared interfaces can require a much broader suite. Dependency information can guide selection, but periodic complete regression runs remain important because indirect interactions may not be captured perfectly by automated impact analysis.

The CI pipeline should enforce reproducibility while recognizing that some robotics tests require specialized resources. GPU inference tests, real-time workloads, HIL systems, or licensed simulation environments may not be available on every worker. Such tests can be assigned to dedicated runners or later verification pipelines while the main CI path preserves fast software-only feedback. Resource requirements and skipped tests should remain explicit rather than silently reducing verification scope.

Trend information across CI runs can reveal degradation that individual pass or fail results do not expose. Test duration, initialization time, inference latency, memory consumption, failure frequency, and other selected observations can be tracked across revisions. These measurements are not substitutes for dedicated benchmarking, but significant changes can identify emerging integration problems or infrastructure regressions before they become functional failures.

A successful CI pipeline should produce a traceable verification record linking the source revision, build environment, executed tests, results, and retained evidence. This record supports debugging, release decisions, regression analysis, and later validation activities. When a defect is discovered in simulation or on a physical robot, an appropriate lower-level regression test should be added where possible so the same defect is detected earlier in future development cycles.

An integrated unit and integration test pipeline therefore acts as the automated quality backbone of robot software development. By ordering tests from fast isolated verification to broader software integration, controlling environments, preserving diagnostics, enforcing gates, and continuously executing regression scenarios, CI prevents many software defects from reaching expensive downstream testing and establishes a repeatable foundation for HIL, simulation, validation, benchmarking, and field testing.

로봇 소프트웨어를 위한 지속적 통합(CI, Continuous Integration) 파이프라인은 소프트웨어가 변경될 때마다 실행되는 자동화된 검증 절차에 단위 테스트(Unit Testing)와 통합 테스트(Integration Testing)를 결합한다. 목적은 결함이 시뮬레이션(Simulation), 하드웨어 인더루프(HIL, Hardware-in-the-Loop), 실제 로봇 테스트로 전파되기 전에 탐지하는 것이다. 파이프라인은 소스 코드 변경을 재현 가능한 빌드, 결정론적 테스트(Deterministic Test), 검증 증거 수집(Evidence Collection), 승인 게이트(Acceptance Gate)와 연결하여 소프트웨어 품질을 릴리스 직전에만 평가하는 것이 아니라 지속적으로 평가할 수 있도록 한다.

파이프라인은 검증 범위(Verification Scope)와 실행 비용(Execution Cost)에 따라 테스트를 구성해야 한다. 빠른 단위 테스트는 분산 서비스(Distributed Service)를 요구하지 않고 알고리즘, 유틸리티(Utility), 제어기(Controller), 인지 추론 래퍼(Perception Inference Wrapper), 기타 소프트웨어 구성요소를 격리하므로 일반적으로 가장 먼저 실행한다. 비용이 더 높은 ROS 2 통합, 종단 간(End-to-End), API, 데이터 파이프라인 테스트는 기본적인 소프트웨어 검사가 성공한 이후에만 실행하여 불필요한 컴퓨팅 리소스 소비를 줄이고 개발자에게 결과를 제공하는 시간을 단축한다.

CI 실행은 정의된 소스 리비전(Source Revision)과 재현 가능한 빌드 환경(Reproducible Build Environment)에서 시작해야 한다. 컴파일러 버전, ROS 2 의존성, 미들웨어 구성(Middleware Configuration), Python 패키지, 추론 런타임(Inference Runtime), 외부 라이브러리는 가능한 경우 버전이 관리되는 구성 또는 컨테이너 이미지(Container Image)를 통해 제어해야 한다. 파이프라인은 정확한 소프트웨어 리비전과 관련 환경 정보를 기록하여 실패한 테스트를 이후 동등한 조건에서 재현할 수 있도록 해야 한다.

빌드 단계(Build Stage)는 기능 테스트를 시작하기 전에 패키지가 정상적으로 컴파일되는지를 검증해야 한다. ROS 2 작업공간(Workspace)은 필요한 패키지 의존성과 테스트 옵션을 활성화한 상태에서 빌드할 수 있으며, 프로젝트 정책에 따라 컴파일러 경고와 정적 분석(Static Analysis) 결과도 수집할 수 있다. 테스트 대상 소프트웨어 아티팩트(Software Artifact)를 일관되게 생성할 수 없는 경우 통합 테스트 결과는 의미가 없으므로 빌드 실패 시 종속된 이후 단계를 종료해야 한다.

단위 테스트는 첫 번째 실행 가능한 검증 게이트(Verification Gate)를 구성한다. GoogleTest 또는 유사한 프레임워크를 기반으로 하는 C++ 테스트와 PyTest 기반 Python 테스트를 통해 수학 함수, 상태 머신(State Machine), 제어기 알고리즘, 메시지 처리 로직, 추론 전처리(Inference Preprocessing), 실패 처리(Failure Handling)를 검증할 수 있다. 이러한 테스트는 모든 관련 변경에서 신속하게 실행될 수 있도록 결정론적이어야 하며 불필요한 미들웨어, 네트워크, 데이터베이스 또는 물리적 하드웨어 의존성과 분리되어야 한다.

ROS 2 패키지 테스트는 작업공간 빌드 및 테스트 시스템과 자연스럽게 통합되어야 한다. ament를 통해 등록된 테스트는 자동화된 파이프라인의 일부로 실행할 수 있으며 결과는 기계 판독형(Machine-Readable) 형식으로 수집할 수 있다. 실패한 어설션(Assertion), 프로세스 오류, 패키지 수준 테스트 결과는 아티팩트(Artifact)로 보존해야 한다. 이를 통해 CI 실패에서 회귀(Regression)를 발생시킨 패키지와 테스트 사례까지 즉시 추적할 수 있다.

단위 수준 검증이 성공하면 집중된 ROS 2 노드 그래프 통합 테스트(Node-Graph Integration Test)를 통해 실제 운용 구성요소 사이의 통신을 검증할 수 있다. 파이프라인은 제어된 구성을 사용하여 선택된 퍼블리셔(Publisher), 서브스크라이버(Subscriber), 서비스(Service), 액션(Action), 수명주기 노드(Lifecycle Node), 지원 프로세스를 실행할 수 있다. 테스트는 임의의 지연 시간 대신 관측 가능한 준비 조건(Readiness Condition)을 기다린 후 메시지 교환, 서비스 품질(QoS, Quality of Service) 호환성, 상태 전이, 변환(Transform), 정의된 실패 동작을 검증해야 한다.

종단 간 소프트웨어 시나리오(End-to-End Software Scenario)는 완전한 기능 경로에 걸쳐 파이프라인의 검증 범위를 확장한다. 제어된 내비게이션(Navigation), 조작(Manipulation), 인지(Perception), 임무 작업 흐름(Mission Workflow)에 알려진 입력을 주입하고 중간 체크포인트(Intermediate Checkpoint)와 최종 출력을 관찰할 수 있다. 이러한 시나리오는 실제 운용 환경과 유사한 소프트웨어 구성을 사용하면서 필요한 경우 물리적 하드웨어를 결정론적인 입력원으로 대체해야 한다. 목적은 시뮬레이션이나 실제 환경의 불확실성을 도입하기 전에 조정된 소프트웨어 동작을 검증하는 것이다.

API 통합 단계(API Integration Stage)는 플릿 시스템(Fleet System), 운영자 애플리케이션(Operator Application), 클라우드 서비스(Cloud Service), 외부 자동화 시스템에서 사용하는 REST 및 gRPC 경계를 검증할 수 있다. CI 환경에서는 필요한 API 서비스를 시작하고, 제어된 요청을 전송하며, 스키마(Schema)와 응답을 검증하고, 타임아웃 및 오류 경로를 실행하며, 내부 ROS 2 작업으로의 매핑(Mapping)을 확인할 수 있다. 서로 호환되지 않는 소프트웨어 리비전이 함께 배포되기 전에 계약 오류(Contract Failure)를 탐지해야 한다.

데이터베이스 및 데이터 파이프라인 테스트(Database and Data-Pipeline Test)는 영속성(Persistence)과 정보 흐름(Information Flow)을 검증하기 위한 임시 인프라를 구성할 수 있다. 파이프라인은 스키마를 초기화하고, 결정론적 픽스처(Deterministic Fixture)를 로딩하며, 대표적인 텔레메트리 또는 임무 데이터 흐름을 실행하고, 저장되거나 변환된 결과를 검사할 수 있다. 실행 비용과 변경된 구성요소의 위험 수준에 따라 트랜잭션(Transaction), 직렬화(Serialization), 중복 처리, 순서 처리(Ordering), 마이그레이션(Migration), 복구 시나리오를 포함할 수 있다.

테스트 환경은 상태 누출(State Leakage)을 방지하기 위해 서로 격리되어야 한다. ROS 2 네임스페이스(Namespace), 데이터베이스, 임시 파일, 네트워크 포트, 캐시(Cache), 메시지 큐(Message Queue), 생성된 아티팩트는 공유 작업 환경에서 테스트가 병렬 또는 순차적으로 실행될 때 서로 분리되어야 한다. 실패가 발생하더라도 정리 작업(Cleanup)은 신뢰성 있게 실행되어야 하며, 중단된 시나리오에서 남은 프로세스나 데이터가 이후 CI 작업의 결과를 변경해서는 안 된다.

테스트가 독립적이고 인프라 리소스가 허용하는 경우 병렬화(Parallelization)를 통해 전체 검증 시간을 줄일 수 있다. 단위 테스트 패키지는 대부분 동시에 실행할 수 있지만 통합 시나리오는 CPU, 메모리, 네트워크 리소스, 데이터베이스 또는 GPU를 서로 경쟁적으로 사용할 수 있으므로 더욱 신중한 스케줄링이 필요하다. 리소스 인식 실행(Resource-Aware Execution)은 계산량이 많은 여러 로보틱스 작업이 동일한 작업 환경에서 동시에 실행되었다는 이유만으로 관련 없는 테스트에서 타이밍 실패가 발생하는 것을 방지한다.

불안정한 테스트(Flaky Test)는 무제한 재시도로 숨기는 것이 아니라 엔지니어링 결함(Engineering Defect)으로 다루어야 한다. 임의의 대기 시간, 제어되지 않는 타이밍, 공유 상태, 난수 시드(Random Seed), 디스커버리 경쟁(Discovery Race)으로 인해 간헐적으로 실패하는 테스트는 전체 파이프라인의 신뢰성을 저하시킨다. CI 인프라는 제품 결함과 테스트 환경의 불안정성을 구분할 수 있는 충분한 증거를 보존해야 하며, 재시도를 허용하는 경우에도 횟수를 제한하고 보고 결과에 명확하게 표시해야 한다.

실패 진단 정보(Failure Diagnostics)는 모든 주요 단계에서 자동으로 수집해야 한다. 유용한 증거에는 테스트 보고서(Test Report), 프로세스 로그(Process Log), ROS 2 진단 정보, 메시지 추적(Message Trace), 매개변수 스냅샷(Parameter Snapshot), 데이터베이스 오류, API 응답, 타임스탬프, 코어 덤프(Core Dump), 관련 런타임 메타데이터(Runtime Metadata)가 포함될 수 있다. 아티팩트는 소스 리비전 및 테스트 시나리오와 연결하여 엔지니어가 불완전하게 기록된 CI 환경을 먼저 재현하지 않고도 회귀 문제를 조사할 수 있도록 해야 한다.

커버리지 정보(Coverage Information)는 실행된 소프트웨어 경로와 테스트되지 않은 경로를 식별하여 테스트 결과를 보완할 수 있다. 라인 커버리지(Line Coverage), 분기 커버리지(Branch Coverage), 함수 커버리지(Function Coverage)는 중요한 테스트 공백을 발견하는 데 도움을 줄 수 있지만 커버리지 비율 자체를 동작 정확성의 증거로 간주해서는 안 된다. 전체적인 수치 커버리지가 높더라도 안전 관련 오류 처리, 경계 조건(Boundary Condition), 상태 전이, 인터페이스 계약에는 명시적인 테스트 시나리오가 필요하다.

파이프라인 게이트(Pipeline Gate)는 로봇 소프트웨어의 중요도(Criticality)와 성숙도(Maturity)를 반영해야 한다. 풀 리퀘스트(Pull Request)에서는 성공적인 컴파일과 모든 빠른 단위 테스트를 요구할 수 있으며, 보호된 브랜치(Protected Branch)로 병합할 때는 ROS 2 통합 테스트와 선택된 종단 간 시나리오를 추가로 요구할 수 있다. 릴리스 후보(Release Candidate)는 더욱 광범위한 API, 데이터베이스, 복구, 호환성 및 회귀 테스트 스위트를 실행할 수 있다. 이러한 계층화 정책(Layered Policy)은 빠른 개발자 피드백과 점진적으로 포괄적인 검증 사이의 균형을 제공한다.

소프트웨어 저장소가 대규모화되면 변경 인식 테스트 선택(Change-Aware Test Selection)을 통해 효율성을 향상시킬 수 있다. 제어기 라이브러리의 변경은 해당 단위 테스트와 종속된 ROS 2 통합 시나리오를 즉시 실행하도록 할 수 있으며, 공유 인터페이스 변경은 훨씬 광범위한 테스트 스위트를 요구할 수 있다. 의존성 정보를 사용하여 테스트 선택을 결정할 수 있지만 자동 영향 분석(Impact Analysis)이 간접적인 상호작용을 완벽하게 파악하지 못할 수 있으므로 주기적인 전체 회귀 테스트(Full Regression Test)는 여전히 중요하다.

CI 파이프라인은 일부 로보틱스 테스트가 특수한 리소스를 요구한다는 점을 고려하면서도 재현성을 보장해야 한다. GPU 추론 테스트, 실시간 작업 부하(Real-Time Workload), HIL 시스템 또는 라이선스가 필요한 시뮬레이션 환경은 모든 작업 환경에서 사용할 수 없을 수 있다. 이러한 테스트는 전용 러너(Dedicated Runner) 또는 이후 검증 파이프라인에 할당하고, 기본 CI 경로에서는 빠른 소프트웨어 전용 피드백을 유지할 수 있다. 리소스 요구사항과 실행되지 않은 테스트는 검증 범위를 조용히 축소하는 대신 명시적으로 표시해야 한다.

여러 CI 실행에 걸친 추세 정보(Trend Information)는 개별 합격 또는 불합격 결과만으로는 드러나지 않는 성능 저하를 보여줄 수 있다. 테스트 실행 시간, 초기화 시간, 추론 지연시간(Inference Latency), 메모리 사용량, 실패 빈도 및 기타 선택된 관측값을 리비전 전체에 걸쳐 추적할 수 있다. 이러한 측정값은 전용 벤치마킹(Benchmarking)을 대체하지 않지만 큰 변화가 발생하면 기능적 실패로 발전하기 전에 새로운 통합 문제 또는 인프라 회귀(Infrastructure Regression)를 식별할 수 있다.

성공적인 CI 파이프라인은 소스 리비전, 빌드 환경, 실행된 테스트, 결과, 보존된 검증 증거를 연결하는 추적 가능한 검증 기록(Traceable Verification Record)을 생성해야 한다. 이러한 기록은 디버깅(Debugging), 릴리스 결정, 회귀 분석, 이후 검증 활동을 지원한다. 시뮬레이션 또는 실제 로봇에서 결함이 발견되면 가능한 경우 적절한 하위 수준 회귀 테스트를 추가하여 이후 개발 주기에서는 동일한 결함을 더 이른 단계에서 탐지할 수 있도록 해야 한다.

통합된 단위 및 통합 테스트 파이프라인은 로봇 소프트웨어 개발을 위한 자동화된 품질 관리의 핵심 기반(Automated Quality Backbone)으로 기능한다. 빠르고 격리된 검증에서 보다 광범위한 소프트웨어 통합으로 테스트 순서를 구성하고, 환경을 제어하며, 진단 정보를 보존하고, 검증 게이트를 적용하며, 회귀 시나리오를 지속적으로 실행함으로써 CI는 많은 소프트웨어 결함이 비용이 높은 후속 테스트 단계까지 전달되는 것을 방지한다. 이를 통해 HIL, 시뮬레이션, 검증(Validation), 벤치마킹, 현장 테스트(Field Testing)를 위한 반복 가능하고 신뢰할 수 있는 기반을 구축할 수 있다.
