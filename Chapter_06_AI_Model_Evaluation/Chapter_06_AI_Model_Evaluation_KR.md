**Volume 25. Testing Validation and Benchmarking**

# Chapter 06. AI Model Evaluation

## 06.01. AI Model Evaluation Principles for Robots

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

로봇을 위한 인공지능 모델 평가(AI Model Evaluation)는 학습된 모델이 단순히 오프라인 데이터셋(Offline Dataset)에서 높은 정확도를 달성하는지를 확인하는 것이 아니라, 신뢰할 수 있는 물리적 행동(Physical Behavior)을 지원할 수 있는지를 판단해야 한다. 로봇은 인식(Perception), 추론(Reasoning), 계획(Planning), 행동(Action)을 폐루프(Closed Loop)로 연결하므로 모델의 오류가 실제 움직임과 환경과의 상호작용으로 전파될 수 있다. 따라서 평가는 모델 수준 성능(Model-Level Performance)을 작업 성공(Task Success), 운영 제약(Operational Constraints), 시스템 수준 결과(System-Level Consequences)와 연결해야 한다.

가장 기본적인 원칙은 평가 지표(Metric)를 선택하기 전에 의도된 운영 영역(Operational Domain)을 정의하는 것이다. 평가 명세(Evaluation Specification)에는 로봇 유형, 작업, 환경, 센서 구성, 객체 클래스, 인간과의 상호작용, 운영 속도, 예상되는 외란(Disturbance)이 포함되어야 한다. 통제된 실험실에서 우수한 성능을 보이는 모델도 실제 배치 환경에서 발생하는 조명 변화, 혼잡, 진동, 센서 잡음, 지형 변화 또는 익숙하지 않은 객체에 대해서는 실패할 수 있다.

평가 데이터셋(Evaluation Dataset)은 정상적인 운영 조건뿐 아니라 운영 영역의 경계에 가까운 어려운 조건까지 표현해야 한다. 정보 누출(Data Leakage)을 방지하기 위해 학습 데이터(Training Data), 검증 데이터(Validation Data), 테스트 데이터(Test Data)를 신중하게 분리해야 하며, 테스트 세트(Test Set)에는 장면, 시점, 객체, 궤적, 사용자, 환경 상태의 의미 있는 변화가 포함되어야 한다. 또한 로봇 평가에서는 개별 샘플을 독립적으로 평가할 때 손실될 수 있는 시간적·공간적 관계(Temporal and Spatial Relationships)를 보존해야 한다.

하나의 지표만으로 로봇 인공지능 모델(Robotic AI Model)의 특성을 충분히 평가할 수는 없다. 인식 시스템(Perception System)은 정확도(Accuracy), 정밀도(Precision), 재현율(Recall), 교차영역비(IoU), 위치 추정 오차(Localization Error), 보정(Calibration), 시간적 일관성(Temporal Consistency)을 요구할 수 있다. 반면 내비게이션 정책(Navigation Policy)은 성공률, 경로 효율성, 충돌, 목표 오차와 관련된 측정이 필요하며, 조작(Manipulation)과 이동(Locomotion)은 작업 완료율, 안정성, 기민성(Dexterity), 속도, 제어 품질(Control Quality) 등의 추가 지표를 필요로 한다.

모델 평가는 구성요소 품질(Component Quality)과 종단간 작업 성능(End-to-End Task Performance)을 구분해야 한다. 인식 모델이 이미지 수준 지표(Image-Level Metric)를 개선하더라도 내비게이션이나 조작 성능이 실제로 향상되지 않을 수 있으며, 통계적으로 작은 인식 오류가 심각한 하위 시스템 오류(Downstream Failure)를 유발할 수도 있다. 따라서 평가는 예측 오류가 상태 추정(State Estimation), 계획 결정(Planning Decision), 제어 명령(Control Command), 물리적 접촉(Physical Contact), 그리고 최종적인 로봇 임무의 성공 또는 실패에 어떠한 영향을 주는지 추적해야 한다.

로봇 인공지능(Robotic AI)은 물리적 실험에 상당한 변동성(Variability)이 존재하므로 반복 시험(Repeated Trial)을 통해 평가해야 한다. 초기 로봇 자세, 객체 배치, 마찰, 센서 잡음, 네트워크 상태, 인간 행동, 액추에이터 응답(Actuator Response)은 소프트웨어가 동일하더라도 결과를 변화시킬 수 있다. 평균 성능만 보고하면 불안정한 행동을 감출 수 있으므로 가능한 경우 분포(Distribution), 분산(Variance), 신뢰구간(Confidence Interval), 실패 빈도, 최악 조건 결과(Worst-Case Outcome), 반복성(Repeatability)을 종합 점수와 함께 제시해야 한다.

일반화(Generalization)는 로봇이 학습 분포(Training Distribution)와 다른 상황을 필연적으로 접하기 때문에 특히 중요하다. 평가에서는 모든 테스트마다 모델을 재학습하지 않고 객체, 환경, 배경, 명령, 시점, 적재물, 지형, 상호작용 패턴 등을 변화시켜야 한다. 분포 내(In-Distribution) 조건과 분포 외(Out-of-Distribution, OOD) 조건의 결과를 별도로 보고하면 성능이 실제로 전이 가능한 능력(Transferable Capability)을 반영하는지, 아니면 특정 벤치마크 패턴에 대한 제한적인 적응을 나타내는지 파악할 수 있다.

강건성 평가(Robustness Evaluation)는 실제 배치된 로봇이 경험할 수 있는 교란(Perturbation)을 의도적으로 도입한다. 영상은 흐림, 눈부심, 어두운 환경, 가림(Occlusion), 오염 또는 프레임 손실(Dropped Frame)의 영향을 받을 수 있으며, 위치 추정 입력에는 드리프트(Drift)나 측정값 누락이 발생할 수 있다. 통신에서는 지연시간(Latency)이나 패킷 손실(Packet Loss)이 발생할 수 있고, 물리 시스템은 외란과 동역학 변화에 노출된다. 목표는 성능이 언제 저하되는지를 확인하는 것뿐 아니라 성능 저하가 얼마나 점진적이고 예측 가능하게 발생하는지 특성화하는 것이다.

안전성(Safety)은 정상적인 작업 성능(Nominal Task Performance)과 독립적으로 평가해야 한다. 두 모델이 비슷한 성공률을 보이더라도 한 모델이 간헐적으로 위험한 움직임을 생성하거나, 사람을 무시하거나, 장애물에 지나치게 접근하거나, 불확실한 상황에서 통제되지 않은 행동을 생성한다면 위험 프로파일(Risk Profile)은 크게 다를 수 있다. 따라서 평가는 안전 중요 실패 모드(Safety-Critical Failure Mode)를 식별하고 측정 가능한 제약 조건을 설정하며, 위반 사항을 기록하고, 위험한 행동이 발생하기 전에 신뢰도 추정(Confidence Estimation) 또는 폴백 메커니즘(Fallback Mechanism)을 통해 로봇이 안전 상태(Safe State)로 전환할 수 있는지를 검토해야 한다.

불확실성(Uncertainty)과 보정(Calibration)은 모델 품질을 평가하는 또 다른 중요한 차원을 제공한다. 이상적으로 로봇은 모든 출력을 동일하게 신뢰하는 대신 확신할 수 있는 예측과 모호한 상황을 구분할 수 있어야 한다. 보정 분석(Calibration Analysis)은 예측된 신뢰도와 실제 정확성을 비교하며, 거부 임계값(Rejection Threshold), 중복 센싱(Redundant Sensing), 인간 개입(Human Intervention), 보수적 계획(Conservative Planning)을 지원할 수 있다. 이는 익숙하지 않은 조건에서 기존 정확도 측정만으로 운영 의사결정을 수행하기 어려울 때 특히 중요하다.

실시간 성능(Real-Time Performance)은 로봇 분야에서 모델 정확성(Model Correctness)의 일부로 간주되어야 한다. 정확도가 매우 높은 모델이라도 결과 생성이 지나치게 느리면 오래된 관측값(Stale Observation)이나 지연된 행동을 생성하여 폐루프 안정성(Closed-Loop Stability)과 안전성을 저하시킬 수 있다. 평가는 워크스테이션 측정에만 의존하지 않고 실제 배치 하드웨어(Deployment Hardware)에서 종단간 지연시간(End-to-End Latency), 지터(Jitter), 처리량(Throughput), 메모리 사용량, 가속기 활용률(Accelerator Utilization), 시작 동작, 계산 부하를 측정해야 한다. 전력 제약이 있는 이동형 시스템에서는 에너지 효율(Energy Efficiency)도 고려해야 한다.

평가는 물리적 현실성(Physical Realism)이 단계적으로 증가하는 환경을 통해 진행되어야 한다. 오프라인 데이터셋 테스트(Offline Dataset Test)는 빠르고 재현 가능한 비교를 제공하고, 시뮬레이션(Simulation)은 대규모 시나리오 변화를 가능하게 하며, 하드웨어 인 더 루프(Hardware-in-the-Loop, HIL) 테스트는 타이밍과 인터페이스 동작을 검증한다. 통제된 물리 시험(Controlled Physical Test)은 모델에서 누락될 수 있는 실제 효과를 드러내며, 최종적인 현장 평가(Field Evaluation)는 실제 운영 환경의 변동성에서도 모델이 효과적으로 동작하는지를 판단한다.

모델 버전 간 비교(Model Version Comparison)를 수행하려면 통제된 실험 조건(Controlled Experimental Conditions)이 필요하다. 데이터셋 버전, 난수 시드(Random Seed), 전처리(Preprocessing), 센서 보정(Sensor Calibration), 하드웨어 구성, 추론 정밀도(Inference Precision), 소프트웨어 의존성, 임계값, 평가 스크립트(Evaluation Script)를 기록해야 한다. 기준 모델(Baseline)은 동등한 조건에서 실행되어야 하며, 가능한 경우 최종 결과를 확인하기 전에 합격 기준(Acceptance Criteria)을 정의해야 한다. 이러한 방식은 벤치마크 조작을 줄이고 연속적인 모델 릴리스(Model Release) 사이에서 의미 있는 회귀 분석(Regression Analysis)을 가능하게 한다.

실패 분석(Failure Analysis)은 종합 점수 계산만큼 중요하다. 평가 기록에는 센서 스트림(Sensor Stream), 모델 입력과 출력, 타임스탬프(Timestamp), 로봇 상태, 명령, 환경 조건, 관련 시스템 이벤트를 보존하여 실패 상황을 재구성할 수 있도록 해야 한다. 이후 오류를 인식 모호성(Perception Ambiguity), 분포 이동(Distribution Shift), 계획 오류, 지연시간, 센서 성능 저하, 상호작용 실패 등의 범주로 분류할 수 있다. 이러한 실패 분류 체계(Failure Taxonomy)는 평가를 단순한 모델 순위 결정에서 전체 로봇 시스템을 개선하기 위한 공학적 과정으로 전환한다.

모델 품질이 자동화된 지표만으로 완전히 표현하기 어려운 상호작용 특성에 의존하는 경우 인간 평가(Human Evaluation)가 필요하다. 인간-로봇 상호작용(Human-Robot Interaction, HRI)에서는 명령 이해, 예측 가능성, 행동의 적절성, 체감 응답성(Perceived Responsiveness), 작업 부담(Workload), 개입 빈도(Intervention Frequency) 등을 평가할 수 있다. 주관적 관찰이 객관적인 시스템 증거를 대체하지 않으면서 정량적 측정을 보완할 수 있도록 인간 평가는 사전에 정의된 프로토콜과 일관된 평가 기준을 사용해야 한다.

성숙한 평가 프로세스(Mature Evaluation Process)는 테스트를 일회성 벤치마크가 아니라 수명주기(Lifecycle)로 취급한다. 새로운 현장 실패, 어려운 시나리오, 새롭게 발견된 분포 이동, 대표적인 운영 데이터를 지속적으로 회귀 테스트 스위트(Regression Test Suite)에 반영해야 한다. 모델 업데이트는 기존 기준 모델과 비교하여 기능, 강건성, 안전성, 지연시간, 효율성 전반의 개선과 회귀(Regression)를 탐지해야 한다. 이를 통해 배치 전 모델 평가(Pre-Deployment Model Evaluation)를 실제 배치 이후의 지속적 테스트(Continuous Testing) 및 모니터링(Monitoring)과 연결할 수 있다.

궁극적으로 로봇을 위한 인공지능 모델 평가(AI Model Evaluation for Robots)는 해당 모델이 의도된 물리적 역할을 수행하기에 충분한 능력(Capability), 강건성(Robustness), 효율성(Efficiency), 예측 가능성(Predictability), 안전성(Safety)을 갖추었는지를 판단해야 한다. 가장 강력한 평가 프레임워크(Evaluation Framework)는 구성요소 지표와 작업 수준 결과, 통제된 벤치마크와 현실적인 시험, 정상 성능과 엣지 케이스(Edge Case), 평균 결과와 실패 분석을 결합한다. 이러한 증거 중심 접근법(Evidence-Centered Approach)은 모델 선택, 배치 결정, 회귀 관리, 지속적인 개선을 위한 방어 가능하고 체계적인 근거를 제공한다.

## 06.02. Perception Model Evaluation mAP IoU ATE [w/Code]

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

인식 모델 평가(Perception Model Evaluation)는 로봇이 원시 센서 관측값(Raw Sensor Observation)을 하위 단계의 위치 추정(Localization), 계획(Planning), 조작(Manipulation), 제어(Control) 모듈이 신뢰할 수 있는 표현으로 얼마나 정확하게 변환하는지를 판단한다. 인식에는 객체 탐지(Object Detection), 분할(Segmentation), 자세 추정(Pose Estimation), 추적(Tracking), 위치 추정이 포함되므로 각각의 출력 유형에 적합한 평가 지표가 필요하다. 평균 정밀도(mAP), 교차영역비(IoU), 절대 궤적 오차(ATE)와 같은 대표적인 지표는 서로 다른 측면의 예측 품질을 측정하므로 전체 인식 성능을 나타내는 상호 대체 가능한 지표로 해석해서는 안 된다.

평균 정밀도(mean Average Precision, mAP)는 카메라 영상, 라이다(LiDAR) 포인트 클라우드(Point Cloud), 다중모달 센서 데이터(Multimodal Sensor Data)를 처리하는 객체 탐지 모델(Object Detection Model)을 평가하는 데 널리 사용된다. 이 지표는 정의된 매칭 기준(Matching Criteria)에 따라 정밀도(Precision)와 재현율(Recall)의 관계를 결합하여 여러 객체 클래스의 탐지 성능을 요약한다. 일반적으로 예측 객체의 클래스와 정답 주석(Ground-Truth Annotation)의 공간적 대응 관계가 평가 임계값을 만족하면 올바른 탐지로 간주하며, 대응되지 않은 예측과 탐지하지 못한 객체는 각각 거짓 양성(False Positive)과 거짓 음성(False Negative)에 반영된다.

정밀도(Precision)는 예측된 탐지 결과 가운데 얼마나 많은 결과가 올바른지를 측정하며, 재현율(Recall)은 실제 정답 객체 가운데 얼마나 많은 객체를 성공적으로 탐지했는지를 측정한다. 모델의 신뢰도 임계값(Confidence Threshold)을 높이면 불확실한 예측을 제거하여 정밀도가 향상될 수 있지만, 동시에 유효한 탐지까지 제거되어 재현율이 감소할 수 있다. 따라서 정밀도-재현율 곡선(Precision-Recall Curve)은 하나의 동작 지점보다 더 많은 정보를 제공하며, 평균 정밀도(Average Precision)는 여러 신뢰도 임계값에서의 성능을 통합하여 올바른 탐지를 잘못된 탐지보다 높은 순위에 배치하는 탐지기의 능력을 나타낸다.

평균 정밀도(mAP)는 여러 클래스에 대한 평균 정밀도(Average Precision) 값을 통합하며, 벤치마크 프로토콜(Benchmark Protocol)에 따라 여러 중첩 임계값(Overlap Threshold)에 대한 결과까지 함께 집계할 수 있다. 동일한 모델이라도 평가 규칙에 따라 점수가 크게 달라질 수 있으므로 보고된 결과에는 정확한 mAP 정의가 반드시 포함되어야 한다. 로봇 개발자는 모델 간 비교의 재현성과 기술적 의미를 유지하기 위해 클래스 정의, 신뢰도 임계값, 중첩 기준, 무시 영역(Ignored Region), 최소 객체 크기, 데이터셋 버전을 기록해야 한다.

교차영역비(Intersection over Union, IoU)는 예측 영역과 정답 영역 사이의 공간적 일치 정도를 평가한다. 경계 상자(Bounding Box) 또는 분할 영역(Segmentation Region)의 경우 IoU는 두 영역의 교집합 면적을 합집합 면적으로 나누어 계산한다. 1에 가까운 값은 높은 공간적 일치를 의미하며, 0에 가까운 값은 중첩이 거의 없음을 의미한다. 따라서 IoU는 직접적인 분할 평가 지표로 사용하거나 객체 탐지 결과를 참 양성(True Positive)으로 판단하기 위한 매칭 기준으로 사용할 수 있다.

로봇 응용 분야에서는 동일한 IoU 값이라도 운영상 서로 다른 결과를 가져올 수 있으므로 주의해서 해석해야 한다. 큰 객체에서는 작은 위치 오차가 발생해도 높은 중첩 점수를 유지할 수 있지만, 작은 객체에서는 동일한 절대 위치 오차가 IoU를 크게 감소시킬 수 있다. 따라서 가느다란 구조물, 부분적으로 가려진 객체, 멀리 떨어진 장애물, 파지 대상(Grasp Target), 안전 중요 영역(Safety-Critical Region)은 데이터셋 전체의 단일 평균 IoU에 의존하기보다 클래스별 분석(Class-Specific Analysis)이 필요할 수 있다.

의미론적 분할 평가(Semantic Segmentation Evaluation)는 일반적으로 각 클래스의 IoU를 보고한 다음 평가 대상 클래스 전체에 대한 평균 IoU(mean IoU)를 계산한다. 이러한 방법은 넓은 배경 영역이 픽셀 수준 정확도(Pixel-Level Accuracy)를 과도하게 지배하는 것을 방지하고 중요한 의미론적 범주가 올바르게 표현되는지를 보다 명확하게 보여준다. 로봇에서는 바닥, 장애물, 사람, 차량, 조작 가능한 객체(Manipulable Object), 미확인 영역(Unknown Region) 또는 기타 작업별 클래스의 결과를 별도로 보고함으로써 높은 종합 분할 점수에 가려진 취약점을 발견할 수 있다.

위치 추정(Localization)과 궤적 추정(Trajectory Estimation) 시스템은 출력이 시간에 따라 지속적으로 변화하기 때문에 서로 다른 평가 지표를 필요로 한다. 절대 궤적 오차(Absolute Trajectory Error, ATE)는 평가 프로토콜에서 요구하는 정렬(Alignment)을 적용한 후 추정 궤적과 정답 기준 궤적(Ground-Truth Reference Trajectory) 사이의 차이를 측정한다. 이는 누적된 위치 및 자세 오차가 내비게이션 성능에 영향을 미치는 시각 주행 거리 측정(Visual Odometry), 동시적 위치 추정 및 지도 작성(SLAM), 시각-관성 추정(Visual-Inertial Estimation) 등의 시스템에서 일반적으로 사용된다.

절대 궤적 오차(ATE)는 일반적으로 시간 동기화된 추정 궤적과 기준 궤적의 자세 차이(Pose Difference)를 이용하여 계산하며, 제곱평균제곱근 오차(Root Mean Square Error), 평균, 중앙값, 표준편차 또는 최대 오차 등의 통계량으로 요약한다. ATE를 계산하기 전에 타임스탬프 연계(Timestamp Association), 좌표계(Coordinate Frame), 궤적 정렬, 스케일 처리(Scale Handling), 누락 자세(Missing Pose)의 처리 방법을 정의해야 한다. 이러한 규칙이 없으면 동일한 기록 시퀀스를 사용하더라도 서로 다른 시스템이나 실험의 ATE 값을 신뢰성 있게 비교할 수 없다.

낮은 절대 궤적 오차(ATE)가 모든 순간에 우수한 동작을 보장하는 것은 아니다. 궤적 정렬과 종합 통계는 국부적인 실패(Local Failure)를 감출 수 있기 때문이다. 위치 추정 시스템은 전체적으로 허용 가능한 오차를 보이면서도 일시적인 위치 점프, 드리프트(Drift), 추적 손실(Tracking Loss), 복구 지연(Delayed Recovery)을 경험하여 로봇 제어를 불안정하게 만들 수 있다. 따라서 하나의 ATE 요약값만 보고하는 것이 아니라 궤적의 수치적 분석, 구간별 오차, 추적 가용성(Tracking Availability), 복구 동작, 오차 분포를 함께 평가해야 한다.

인식 평가에서는 시간적 일관성(Temporal Consistency)도 고려해야 한다. 올바른 분류와 잘못된 분류를 프레임마다 빠르게 반복하는 탐지기는 프레임 수준 mAP가 양호하더라도 불안정한 객체 추적과 계획 결정을 발생시킬 수 있다. 마찬가지로 프레임 사이에서 분할 경계가 흔들리면 장애물 지도에 영향을 줄 수 있으며, 간헐적인 위치 추정 오류는 급격한 궤적 수정을 유발할 수 있다. 따라서 이러한 특성이 로봇 동작에 영향을 주는 경우 시퀀스 기반 테스트(Sequence-Based Testing)를 통해 지속성(Persistence), 추적 연속성(Track Continuity), 예측 안정성(Prediction Stability), 실패 지속시간(Failure Duration)을 측정해야 한다.

평가 데이터셋(Evaluation Dataset)은 실제 로봇 운영 중 예상되는 조건을 표현해야 한다. 객체 탐지 및 분할 테스트에는 관련성이 있는 경우 조명, 거리, 시점, 모션 블러(Motion Blur), 혼잡, 가림(Occlusion), 객체 크기, 날씨, 센서 오염 등의 변화가 포함되어야 한다. 위치 추정 데이터셋에는 다양한 궤적, 운동 동역학(Motion Dynamics), 텍스처, 기하학적 구조, 성능이 저하된 센싱 조건을 포함해야 한다. 조건별 성능을 별도로 보고하면 종합적인 mAP, IoU 또는 ATE 결과가 쉬운 시나리오에 의해 과도하게 좌우되는지를 확인할 수 있다.

분포 외 평가(Out-of-Distribution Evaluation, OOD Evaluation)는 배치 환경에서 학습 데이터에 존재하지 않았던 객체와 시각적 구성이 지속적으로 등장하기 때문에 인식 시스템에서 특히 중요하다. 모델은 익숙하지 않은 객체 인스턴스, 새로운 배경, 변화된 조명, 변경된 센서 특성, 기존에 익숙했던 요소들의 비정상적인 조합을 대상으로 테스트해야 한다. 또한 높은 신뢰도를 가진 잘못된 예측은 물리적 로봇에서 명시적인 불확실성보다 더 위험할 수 있으므로 신뢰도 보정(Confidence Calibration)과 미확인 객체 처리(Unknown-Object Behavior)도 평가해야 한다.

인식 지표(Perception Metric)는 궁극적으로 하위 단계의 작업 결과(Downstream Task Outcome)와 연결되어야 한다. mAP의 변화는 장애물 탐지, 사람 인식, 조작 대상 선택 또는 다른 로봇 기능을 실제로 변화시킬 때 중요한 의미를 갖는다. IoU 향상은 자유 공간 추정(Free-Space Estimation)이나 파지 형상(Grasp Geometry)에 미치는 영향과 함께 검토해야 하며, ATE 감소는 내비게이션 정확도와 지도 일관성(Map Consistency)의 향상과 연계하여 평가해야 한다. 이러한 시스템 수준 해석(System-Level Interpretation)은 실제 로봇 동작을 거의 개선하지 못하는 벤치마크 수치만을 최적화하는 문제를 방지한다.

실행시간 특성(Runtime Characteristics)도 인식 평가의 중요한 부분이다. 객체 탐지, 분할, 위치 추정 모델은 실시간 제어 파이프라인(Real-Time Control Pipeline) 내부에서 동작하는 경우가 많으므로 예측 정확도뿐 아니라 추론 지연시간(Inference Latency), 처리량(Throughput), 지터(Jitter), 메모리 사용량, 가속기 활용률(Accelerator Utilization)도 중요하다. 이러한 지표는 대표적인 실제 배치 하드웨어(Deployment Hardware)와 현실적인 센서 주기에서 측정해야 한다. 필요한 처리 주파수를 유지하지 못하는 고정확도 인식 모델은 오래된 정보를 전달하여 폐루프 로봇 성능(Closed-Loop Robot Performance)을 저하시킬 수 있다.

강건한 평가 보고서(Robust Evaluation Report)는 결과 지표와 함께 전체 실험 환경(Experimental Context)을 보존해야 한다. 모델 버전, 데이터셋 버전, 센서 구성, 전처리(Preprocessing), 입력 해상도, 신뢰도 설정, 매칭 임계값, 하드웨어 플랫폼, 수치 정밀도(Numerical Precision), 평가 소프트웨어를 기록해야 한다. 이를 통해 mAP, IoU, ATE는 단순히 분리된 벤치마크 수치가 아니라 재현 가능한 공학적 증거(Reproducible Engineering Evidence)로 활용될 수 있으며, 모델 비교, 회귀 탐지(Regression Detection), 배치 결정, 로봇 인식 시스템의 지속적인 개선을 지원할 수 있다.

## 06.03. Navigation Policy Evaluation SR SPL NE [w/Code]

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

내비게이션 정책 평가(Navigation Policy Evaluation)는 로봇이 인식(Perception), 위치 추정(Localization), 지도 정보(Map Information), 작업 목표(Task Objective)를 목적지를 향한 신뢰성 있는 움직임으로 변환할 수 있는지를 판단한다. 독립적인 예측 모델을 평가하는 것과 달리 내비게이션 평가는 하나의 에피소드(Episode) 동안 이루어지는 전체 의사결정 순서를 고려해야 한다. 성공률(Success Rate, SR), 경로 길이 가중 성공률(Success weighted by Path Length, SPL), 내비게이션 오차(Navigation Error, NE)는 각각 작업 완료, 경로 효율성, 최종 목표 정확도를 상호 보완적으로 측정한다.

성공률(Success Rate, SR)은 전체 내비게이션 에피소드 중 로봇이 사전에 정의된 성공 조건(Success Condition)을 만족한 비율을 측정한다. 지점 목표 내비게이션(Point-Goal Navigation)에서는 일반적으로 로봇이 중요 제약 조건을 위반하지 않으면서 목표로부터 지정된 거리 이내에서 정지하면 성공으로 판단한다. 실제 시스템에서는 충돌 없는 운행, 유효한 위치 추정, 제한시간 이내의 완료 또는 올바른 정지 결정(Stopping Decision) 수행 등이 추가적인 성공 조건으로 요구될 수 있다.

실험을 시작하기 전에 성공 조건을 명확하게 정의해야 한다. 사소해 보이는 기준의 차이도 보고되는 성공률(SR)을 크게 변화시킬 수 있기 때문이다. 목표 허용 오차(Goal Tolerance), 최대 에피소드 지속시간, 충돌 제한, 복구 허용 조건(Recovery Allowance), 종료 규칙(Termination Rule)은 비교 대상 정책 전체에서 일관되게 유지해야 한다. 목표 영역에 도달했지만 도착을 인식하지 못한 로봇과 목표에 전혀 접근하지 못한 로봇은 단순한 종합 점수에서는 모두 실패로 나타날 수 있지만 서로 다른 유형의 실패로 분류할 필요가 있다.

성공률(SR)은 직관적인 지표이지만 성공한 정책이 얼마나 효율적으로 목적지에 도달했는지는 측정하지 못한다. 두 정책이 동일한 SR을 달성하더라도 하나는 짧고 직접적인 궤적을 따르는 반면 다른 하나는 반복적으로 우회하거나 진동하거나 불필요한 복구 동작을 수행할 수 있다. 이러한 차이는 임무 시간, 에너지 소비, 교통 상호작용(Traffic Interaction), 플릿 생산성(Fleet Productivity)에 영향을 주므로 이진 성공 여부뿐 아니라 경로 효율성(Path Efficiency) 지표를 함께 사용해야 한다.

경로 길이 가중 성공률(Success weighted by Path Length, SPL)은 내비게이션 성공과 궤적 효율성(Trajectory Efficiency)을 결합한다. 성공한 에피소드에서는 실제 이동 경로가 실행 가능한 최단 기준 경로(Shortest Feasible Reference Path)에 가까울수록 높은 점수를 받고, 불필요한 이동 거리가 증가할수록 낮은 점수를 받는다. 실패한 에피소드는 일반적으로 성공 경로에 대한 점수를 얻지 못한다. 따라서 SPL은 단순히 목적지에 도달하는 정책과 효율적인 경로를 사용하여 지속적으로 목적지에 도달하는 정책을 구분할 수 있다.

SPL 계산에 사용되는 기준 경로(Reference Path)는 신중하게 정의해야 한다. 평가 환경에 따라 기준 경로는 측지 거리(Geodesic Distance), 충돌 없는 최단 경로 또는 알려진 지도에서 생성된 경로를 기반으로 할 수 있다. 로봇 크기, 장애물 팽창(Obstacle Inflation), 운동학적 제약(Kinematic Constraint), 주행 가능성(Traversability), 일방통행 영역 등의 요소 때문에 이론적으로 가장 짧은 기하학적 경로가 실제로는 주행 불가능할 수 있다. 따라서 기준 경로는 평가 대상 플랫폼의 운동 능력과 운영 제약을 반영해야 한다.

내비게이션 오차(Navigation Error, NE)는 로봇의 최종 위치와 목표 위치 사이에 남아 있는 거리를 측정한다. 이 지표는 실패한 에피소드에서도 유용한 정보를 제공한다. 성공 허용 범위를 약간 벗어난 위치에서 정지한 로봇과 목적지에서 멀리 떨어진 상태로 위치를 잃은 로봇을 구분할 수 있기 때문이다. 단순한 성공률만으로는 드러나지 않는 실패의 심각도(Failure Severity)를 확인하기 위해 NE를 평균, 중앙값, 백분위수(Percentile), 최대값 또는 분포 통계(Distributional Statistics)로 보고할 수 있다.

내비게이션 오차(NE)는 작업 특성에 적합한 거리 정의를 사용해야 한다. 개방된 환경에서는 유클리드 거리(Euclidean Distance)가 충분할 수 있지만, 건물, 복도, 다층 구조, 장벽 또는 제한된 지형에서는 측지 거리(Geodesic Distance)가 실제 이동 가능성을 더 잘 반영할 수 있다. 도킹(Docking), 조작, 충전, 검사 또는 인간과의 상호작용을 위해 특정 방향으로 도착해야 하는 경우에는 방향 오차(Orientation Error)도 필요하다. 따라서 목표 달성은 위치 허용 오차와 회전 허용 오차(Rotational Tolerance)를 모두 포함할 수 있다.

성공률(SR), 경로 길이 가중 성공률(SPL), 내비게이션 오차(NE)는 독립적으로 해석하기보다 함께 분석해야 한다. 높은 SR과 낮은 SPL은 신뢰성은 높지만 비효율적인 내비게이션을 나타낼 수 있으며, 중간 수준의 SR과 낮은 NE는 많은 실패가 성공 판정 경계 가까이에서 발생한다는 것을 의미할 수 있다. 높은 SPL을 유지하면서 일부 에피소드에서 매우 큰 오차가 발생한다면 드물지만 심각한 실패가 존재할 수 있다. 이러한 공동 분석(Joint Analysis)은 하나의 지표만 최적화하는 것보다 내비게이션 동작을 더욱 완전하게 평가할 수 있다.

평가 시나리오(Evaluation Scenario)는 의도된 운영 영역(Operational Domain)을 대표하는 다양한 조건을 포함해야 한다. 테스트에서는 경로 길이, 복도 폭, 장애물 밀도, 교차로 복잡성, 지형, 조명, 위치 추정 품질, 센서 가시성(Sensor Visibility), 목표 위치 등을 변화시킬 수 있다. 동적 환경(Dynamic Environment)에서는 필요한 경우 이동하는 사람, 차량 또는 다른 로봇도 포함해야 한다. 시나리오 범주별로 지표를 보고하면 전체적으로 우수해 보이는 내비게이션 성능이 어떤 조건에서 저하되는지를 확인할 수 있다.

내비게이션 정책은 초기 자세, 위치 추정 불확실성(Localization Uncertainty), 이동 장애물, 플래너 타이밍(Planner Timing), 확률적 정책 출력(Stochastic Policy Output)에 민감할 수 있으므로 반복 시험(Repeated Trial)이 필요하다. 재현성이 필요한 경우 난수 시드(Random Seed)를 통제하는 동시에 실제 운영 동작을 특성화할 수 있도록 충분한 변화를 포함해야 한다. 여러 에피소드에서 얻은 신뢰구간(Confidence Interval)과 분포는 제한된 유리한 경로에서 계산한 단일 평균 SR, SPL 또는 NE보다 강력한 평가 근거를 제공한다.

충돌 동작(Collision Behavior)은 목표 중심 지표와 함께 측정해야 한다. 정책이 좁은 간격을 공격적으로 통과하거나 장애물과 빈번하게 접촉하여 높은 성공률을 달성했다고 해서 운영상 우수한 정책으로 평가해서는 안 된다. 평가자는 충돌 횟수, 충돌 심각도, 최소 장애물 이격 거리(Minimum Obstacle Clearance), 비상 정지(Emergency Stop) 작동, 안전 계층 개입(Safety-Layer Intervention), 아차 사고(Near-Miss Event)를 기록하여 허용할 수 없는 물리적 위험 없이 내비게이션 효율성을 달성했는지 판단할 수 있다.

복구 성능(Recovery Performance)은 SR과 SPL만으로 충분히 설명하기 어려운 또 다른 중요한 평가 요소이다. 로봇은 위치 추정 성능 저하, 경로 차단, 일시적인 센서 손실, 플래너 실패 또는 예상하지 못한 장애물을 경험할 수 있다. 평가에서는 내비게이션 시스템이 문제를 탐지하고 적절한 복구 동작(Recovery Behavior)을 시작하며 성공적으로 재계획(Replanning)한 후 다시 이동을 계속하는지 확인해야 한다. 복구 빈도, 복구 지속시간, 반복적인 실패 주기, 최종적인 작업 완료 여부는 유용한 진단 근거를 제공한다.

내비게이션 정책은 일반화(Generalization)와 분포 외 강건성(Out-of-Distribution Robustness)에 대해서도 평가해야 한다. 새로운 지도, 변경된 가구 배치, 익숙하지 않은 장애물 구성, 변화된 센서 잡음, 서로 다른 바닥 조건, 이전에 경험하지 못한 교통 패턴은 학습 환경에 대한 정책의 의존성을 드러낼 수 있다. 분포 내(In-Distribution) 조건과 분포 외(Out-of-Distribution, OOD) 조건의 SR, SPL, NE를 구분하여 평가하면 정책이 전이 가능한 내비게이션 동작(Transferable Navigation Behavior)을 학습했는지 아니면 익숙한 환경 구조를 주로 기억한 것인지 판단할 수 있다.

시뮬레이션(Simulation)은 수천 개의 내비게이션 에피소드를 효율적으로 평가하고 지도, 장애물, 센서, 외란을 체계적으로 변화시킬 수 있는 환경을 제공한다. 그러나 우수한 시뮬레이션 결과가 동일한 물리적 성능을 보장하지는 않는다. 실제 로봇에는 휠 슬립(Wheel Slip), 액추에이터 지연(Actuator Delay), 보정 오차(Calibration Error), 불완전한 센싱, 통신 지터(Communication Jitter), 인간 행동 등 시뮬레이션에서 충분히 표현되지 않을 수 있는 요소가 존재한다. 따라서 내비게이션 평가는 반복 가능한 시뮬레이션 테스트에서 시작하여 통제된 물리 시험과 현장 기반 검증(Field-Based Validation)으로 발전해야 한다.

실행시간 성능(Runtime Performance)은 내비게이션 의사결정이 실시간 제약(Real-Time Constraint)을 만족해야 하므로 행동 지표와 함께 평가해야 한다. 정책 추론 지연시간(Policy Inference Latency), 계획 주파수(Planning Frequency), 제어 업데이트 주기, CPU 및 가속기 활용률, 메모리 사용량, 타이밍 지터(Timing Jitter)는 기반 정책이 동일하더라도 실제 물리적 궤적에 영향을 줄 수 있다. SR, SPL, NE가 제한 없는 컴퓨팅 자원이 아니라 현실적인 배치 조건을 반영하도록 대표적인 실제 로봇 하드웨어에서 측정해야 한다.

완전한 내비게이션 평가 기록(Navigation Evaluation Record)에는 정책 버전, 지도 및 시나리오 식별자, 로봇 구성, 센서 설정, 위치 추정 방법, 성공 허용 오차, 기준 경로 정의, 난수 시드, 소프트웨어 버전, 에피소드 로그(Episode Log)를 보존해야 한다. 또한 궤적, 충돌, 복구 이벤트, 타이밍 정보, 종료 원인(Termination Cause)을 실패 분석에 활용할 수 있도록 유지해야 한다. 이를 통해 SR, SPL, NE를 회귀 테스트(Regression Testing), 정책 비교, 배치 결정을 위한 재현 가능한 공학적 증거(Reproducible Engineering Evidence)로 활용할 수 있다.

궁극적으로 내비게이션 정책 평가(Navigation Policy Evaluation)는 로봇이 단순히 목표에 도달하는지뿐만 아니라 대표적인 운영 조건 전반에서 정확하고 효율적이며 안전하고 일관되게 목표에 도달하는지를 입증해야 한다. 성공률(SR)은 작업 완료를 나타내고, 경로 길이 가중 성공률(SPL)은 경로 효율성을 반영하며, 내비게이션 오차(NE)는 최종적으로 남은 목표 오차를 특성화한다. 이러한 지표를 안전성, 강건성, 복구 능력, 실시간 성능, 시나리오 수준 분석과 결합하면 시뮬레이션부터 검증(Validation), 실제 현장 배치(Field Deployment)에 이르는 자율 내비게이션 정책 평가의 실용적인 기반을 구축할 수 있다.

## 06.04. Manipulation Policy Evaluation SR Dex [w/Code]

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

조작 정책 평가(Manipulation Policy Evaluation)는 로봇이 인식(Perception), 작업 명령(Task Instruction), 객체 상태(Object State), 고유수용성 피드백(Proprioceptive Feedback)을 신뢰할 수 있는 물리적 상호작용(Physical Interaction)으로 변환할 수 있는지를 판단한다. 정적인 예측 작업과 달리 조작은 접근(Reaching), 파지(Grasping), 접촉 제어(Contact Control), 객체 이동(Object Motion), 작업 종료(Task Termination)를 지속적으로 조정해야 한다. 성공률(Success Rate, SR)은 작업 완료를 평가하는 주요 지표이며, 기민성 중심 지표(Dexterity-Oriented Measure)는 복잡한 접촉 및 객체 제어 요구사항을 정책이 얼마나 효과적으로 처리하는지를 평가한다.

성공률(Success Rate, SR)은 전체 조작 시험 중 사전에 정의된 작업 목표(Task Objective)를 만족한 시험의 비율을 측정한다. 픽앤플레이스(Pick-and-Place) 작업에서는 올바른 객체를 파지하여 목표 영역 내부에 배치해야 할 수 있으며, 삽입(Insertion), 붓기(Pouring), 도구 사용(Tool Use), 조립(Assembly)에서는 서로 다른 완료 조건이 요구된다. 성공 정의에는 허용 가능한 최종 객체 자세(Object Pose), 파지 상태(Grasp State), 작업 순서(Task Sequence), 제한시간, 안전 제약 조건, 시험을 즉시 무효화하는 조건 등을 명확하게 지정해야 한다.

이진 성공(Binary Success)은 요청된 물리적 작업이 완료되었는지를 직접적으로 나타내기 때문에 유용하지만 정책 사이의 중요한 차이를 감출 수 있다. 두 정책이 동일한 성공률(SR)을 달성하더라도 하나는 첫 번째 시도에서 작업을 부드럽게 완료하는 반면 다른 하나는 반복적인 파지, 과도한 접촉 또는 긴 복구 과정(Recovery Sequence)에 의존할 수 있다. 따라서 평가에서는 모든 성공 에피소드(Episode)를 동일하게 취급하지 않고 중간 결과와 실행 특성(Execution Characteristics)을 함께 보존해야 한다.

부분 성공 지표(Partial Success Metric)는 장기 작업(Long-Horizon Manipulation)에 대한 추가적인 정보를 제공할 수 있다. 다단계 작업(Multi-Stage Task)은 객체 접근, 안정적인 파지 형성, 들어 올리기, 운반, 정렬, 목표 위치에서 놓기 등의 단계로 구성될 수 있다. 이러한 단계의 완료 여부를 기록하면 실패가 발생하는 위치를 파악하고 인식, 파지, 움직임 생성(Motion Generation), 접촉 제어 문제를 구분할 수 있다. 이러한 분해는 전체 작업 성공률이 상대적으로 낮은 경우 특히 유용하다.

여기서 기민성(Dexterity, Dex)은 단순히 가능한 움직임을 통해 작업을 완료하는 것을 넘어 정밀하고 조화로우며 적응적인 조작을 수행할 수 있는 정책의 능력을 의미한다. 기민성에는 정확한 말단장치 위치 결정(End-Effector Placement), 안정적인 파지 전환(Grasp Transition), 제어된 힘 적용, 손가락 협응(Finger Coordination), 양손 동기화(Bimanual Synchronization), 손 내부 객체 이동(In-Hand Object Motion), 변화하는 접촉 상태에 대한 적응 등이 포함될 수 있다. 따라서 정확한 정의는 로봇의 신체 구조(Embodiment)와 목표 조작 능력에 맞추어 설정해야 한다.

기민성(Dexterity)은 다차원적 특성을 가지므로 명확하게 정의된 평가 프로토콜(Evaluation Protocol)이 없다면 하나의 보편적인 기민성 점수(Dex Score)만으로 충분히 평가하기 어렵다. 실용적인 평가에서는 자세 정확도(Pose Accuracy), 파지 안정성(Grasp Stability), 접촉 품질(Contact Quality), 힘 조절(Force Regulation), 궤적 부드러움(Trajectory Smoothness), 재파지 빈도(Regrasp Frequency), 조작 시간, 기민한 조작 기본 동작(Dexterous Primitive)의 성공적인 실행 등을 결합할 수 있다. 이러한 요소의 가중치와 정규화 방법(Normalization)은 모델 버전 간 기민성 점수를 해석하고 재현할 수 있도록 명확하게 기록해야 한다.

객체 자세 정확도(Object Pose Accuracy)는 정밀한 배치 또는 정렬이 요구되는 조작에서 특히 중요하다. 평가는 작업 실행 후 실제로 달성된 객체 자세와 목표 자세 사이의 병진 오차(Translational Error)와 회전 오차(Rotational Error)를 측정할 수 있다. 페그 삽입(Peg Insertion), 커넥터 결합(Connector Mating), 적층(Stacking), 조립에서는 엄격한 허용 오차가 필요할 수 있지만, 빈 내부에 객체를 배치하는 작업(Bin Placement)에서는 보다 넓은 허용 범위가 적절할 수 있다. 따라서 자세 오차는 작업의 실제 물리적 요구사항에 따라 해석해야 한다.

파지 품질(Grasp Quality)은 그리퍼(Gripper)를 처음 닫는 동작만으로 평가해서는 안 된다. 성공적인 파지는 들어 올리기, 가속, 운반, 방향 변경, 환경과의 상호작용 과정에서도 안정적으로 유지되어야 한다. 평가자는 객체 미끄러짐(Object Slip), 의도하지 않은 회전, 파지 손실(Grasp Loss), 과도한 파지력, 재파지 필요성을 관찰할 수 있다. 기민한 로봇 손(Dexterous Hand)의 경우 손가락 접촉 분포(Finger Contact Distribution)와 서로 다른 파지 구성 사이를 전환하는 능력도 조작 성능을 나타내는 추가적인 근거가 될 수 있다.

접촉 중심 작업(Contact-Rich Task)에서는 힘과 상호작용 동작을 명시적으로 평가해야 한다. 과도한 힘은 객체를 손상시키거나 로봇을 불안정하게 만들거나 안전 위험을 발생시킬 수 있으며, 힘이 부족하면 미끄러짐이나 불완전한 삽입이 발생할 수 있다. 따라서 힘 및 토크 프로파일(Force and Torque Profile), 최대 접촉 하중(Peak Contact Load), 충격량(Impulse), 힘 추종 오차(Force-Tracking Error), 접촉 지속시간(Contact Duration)을 성공률과 함께 평가할 수 있다. 이러한 지표는 조립, 표면 상호작용, 도구 조작, 변형 가능한 객체 처리(Deformable-Object Handling), 사람을 대상으로 하는 조작에서 특히 중요하다.

성공적인 조작이라도 운영 효율성이 낮을 수 있으므로 효율성(Efficiency)도 고려해야 한다. 작업 완료시간, 말단장치 경로 길이(End-Effector Path Length), 관절 움직임, 파지 시도 횟수, 수정 동작(Corrective Action) 횟수, 에너지 소비량 등을 통해 불필요한 동작을 파악할 수 있다. 작업을 빠르게 완료하더라도 위험한 충격을 발생시키는 정책을 자동으로 우수하다고 평가해서는 안 되므로 효율성 지표는 작업 품질, 접촉 안정성, 안전 제약 조건과 함께 해석해야 한다.

조작 평가는 객체 자세, 마찰, 질량 분포, 그리퍼 접촉, 센서 잡음, 로봇 보정(Calibration)의 작은 변화만으로도 결과가 달라질 수 있으므로 반복 시험(Repeated Trial)이 필요하다. 통제된 비교가 필요한 경우 재현성을 유지하면서 초기 조건(Initial Condition)을 체계적으로 변화시켜야 한다. 신뢰구간(Confidence Interval), 결과 분포, 조건별 성공률을 함께 보고하면 소수의 유리한 시연(Demonstration)에서 얻은 단일 종합 성공률보다 더욱 강력한 평가 근거를 제공할 수 있다.

일반화 시험(Generalization Testing)에서는 객체 인스턴스, 형상, 텍스처, 재질, 크기, 질량, 방향, 배치, 주변 혼잡도 등을 변화시켜야 한다. 범용 조작(General-Purpose Manipulation)을 목표로 하는 정책은 학습 과정에서 사용되지 않았던 객체와 구성도 경험해야 한다. 분포 내(In-Distribution) 조건과 분포 외(Out-of-Distribution, OOD) 조건의 성능을 비교하면 정책이 전이 가능한 조작 기술(Transferable Manipulation Skill)을 획득했는지, 아니면 익숙한 객체, 고정된 자세 또는 기억된 시각적 패턴에 크게 의존하는지를 확인할 수 있다.

외란 시험(Disturbance Testing)은 실행이 예상된 궤적에서 벗어났을 때 정책이 조작 진행 상태를 유지하거나 복구할 수 있는지를 평가한다. 접근 과정에서 객체가 이동하거나, 파지가 불완전하거나, 외부 접촉이 로봇 팔에 외란을 발생시키거나, 인식 성능이 일시적으로 저하될 수 있다. 강건한 정책(Robust Policy)은 이러한 변화를 감지하고 움직임이나 힘 제어 전략을 조정하며, 실행 가능한 경우 잘못된 행동 순서를 치명적인 실패까지 계속 수행하지 않고 적절하게 복구할 수 있어야 한다.

로봇 팔과 손은 객체, 장비, 사람과 직접 힘을 교환하므로 안전성 평가(Safety Evaluation)는 조작 성능과 함께 수행되어야 한다. 평가에서는 관절 한계 위반(Joint-Limit Violation), 과도한 속도 또는 토크, 예상하지 못한 충돌, 위험한 접촉력, 객체 낙하, 작업공간 위반(Workspace Violation), 안전 시스템 개입(Safety-System Intervention)을 기록해야 한다. 높은 성공률을 달성하더라도 물리적으로 위험하거나 손상을 유발하는 행동을 통해 성공하는 조작 전략은 적절한 정책으로 평가할 수 없다.

시뮬레이션(Simulation)은 다양한 객체 자세, 물리 매개변수(Physical Parameter), 무작위화된 환경에서 대규모 조작 평가를 수행할 수 있지만 시뮬레이션 접촉 동역학(Contact Dynamics)이 모든 실제 상호작용을 정확하게 재현하는 것은 아니다. 마찰, 순응성(Compliance), 백래시(Backlash), 촉각 응답(Tactile Response), 변형 가능한 재료, 접촉 전환(Contact Transition)은 상당한 시뮬레이션-현실 차이(Simulation-to-Reality Gap)를 발생시킬 수 있다. 따라서 조작 정책은 시뮬레이션 벤치마크에서 통제된 하드웨어 실험과 대표적인 실제 물리 작업 시험으로 단계적으로 확장하여 평가해야 한다.

실행시간 성능(Runtime Performance)도 조작 정책 평가의 중요한 구성요소이다. 비전 기반 또는 다중모달 정책(Multimodal Policy)은 인식, 추론, 행동 생성(Action Generation)에 상당한 계산량을 요구할 수 있으며, 접촉에 민감한 작업에서는 신속한 반응이 필요하다. 정책 추론 지연시간(Policy Inference Latency), 제어 주파수(Control Frequency), 타이밍 지터(Timing Jitter), 메모리 사용량, 가속기 활용률(Accelerator Utilization)을 실제 로봇 하드웨어에서 측정해야 한다. 명목상 정책 예측이 정확하더라도 행동이 지연되면 파지 안정성과 접촉 제어 품질이 저하될 수 있다.

완전한 평가 기록(Evaluation Record)에는 정책 및 모델 버전, 로봇 신체 구조(Robot Embodiment), 그리퍼 또는 로봇 손 구성, 객체 식별자, 초기 자세, 센서 설정, 작업 허용 오차, 무작위화 매개변수(Randomization Parameter), 종료 기준(Termination Criteria)을 보존해야 한다. 또한 로봇 궤적, 관절 상태, 객체 자세, 힘 신호, 정책 출력, 실패 원인, 타이밍 데이터를 기록해야 한다. 이러한 기록은 정책 릴리스 사이에서 성공률 또는 기민성이 변화했을 때 회귀 테스트(Regression Testing)와 상세한 원인 진단을 가능하게 한다.

궁극적으로 조작 정책 평가(Manipulation Policy Evaluation)는 로봇이 물리적 작업을 신뢰성 있게 완료하면서 응용 분야에서 요구하는 정밀도(Precision), 적응성(Adaptability), 효율성(Efficiency), 접촉 제어(Contact Control)를 구현할 수 있는지를 판단해야 한다. 성공률(SR)은 작업 완료 여부를 명확하게 측정하며, 기민성 중심 평가(Dexterity-Oriented Evaluation)는 성공을 달성하기 위해 사용된 물리적 상호작용의 품질을 설명한다. 이러한 지표를 강건성, 안전성, 일반화 능력, 실행시간 분석과 결합하면 실제 배치 전에 조작 정책을 검증하기 위한 실용적인 평가 기반을 구축할 수 있다.

## 06.05. Locomotion Policy Evaluation Speed Stability [w/Code]

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

이동 정책 평가(Locomotion Policy Evaluation)는 다족 로봇(Legged Robot)이 균형을 유지하고 명령된 속도를 추종하며 환경 조건에 적응하면서 신뢰할 수 있는 신체 움직임을 생성할 수 있는지를 판단한다. 정적인 인공지능 평가와 달리 이동은 인식(Perception), 상태 추정(State Estimation), 정책 추론(Policy Inference), 관절 제어(Joint Control), 접촉 동역학(Contact Dynamics), 지형(Terrain) 사이의 지속적인 폐루프 상호작용(Closed-Loop Interaction)으로 평가해야 한다. 따라서 속도(Speed)와 안정성(Stability)은 핵심 지표이지만 안전성, 효율성, 강건성, 작업 완료 성능과 함께 해석해야 한다.

속도 평가(Speed Evaluation)는 로봇이 실제로 구현한 병진 속도(Translational Velocity)와 회전 속도(Rotational Velocity)를 명령된 움직임과 비교하는 것에서 시작한다. 평균 전진 속도(Mean Forward Speed)는 이동성을 나타내는 기본적인 지표이며, 횡방향 속도, 회전 속도, 가속도, 감속도는 보다 광범위한 이동 능력을 나타낸다. 로봇이 짧은 시간 동안 높은 속도에 도달하더라도 장시간 안정적이고 에너지 효율적이며 안전한 이동을 유지하지 못할 수 있으므로 최대 도달 속도(Maximum Achievable Speed)와 지속 가능한 운영 속도(Sustainable Operational Speed)를 구분하여 평가해야 한다.

속도 추종 오차(Velocity Tracking Error)는 이동 정책이 명령된 선형 및 각속도(Linear and Angular Velocity)를 얼마나 정확하게 추종하는지를 측정한다. 하나의 고정 속도에서 우수한 정책도 속도 전환 과정에서는 제대로 반응하지 못할 수 있으므로 일정한 명령, 램프 입력(Ramp Input), 계단형 변화(Step Change), 동적으로 변화하는 기준값을 포함하여 평가해야 한다. 제곱평균제곱근 오차(Root Mean Square Error), 정상상태 오차(Steady-State Error), 오버슈트(Overshoot), 정착시간(Settling Time), 응답 지연(Response Delay)을 통해 명령된 움직임이 예측 가능한 물리적 동작으로 변환되는지를 확인할 수 있다.

안정성 평가(Stability Evaluation)는 로봇이 넘어지거나 과도하게 미끄러지거나 복구할 수 없는 자세에 진입하지 않으면서 제어된 신체 움직임을 유지할 수 있는지를 판단한다. 사족보행 로봇(Quadruped Robot)과 휴머노이드(Humanoid)에서는 베이스 자세(Base Orientation), 롤(Roll) 및 피치(Pitch) 변화, 몸체 높이 편차, 각속도, 발 접촉 일관성(Foot Contact Consistency), 지지 동작(Support Behavior) 등을 평가할 수 있다. 로봇이 넘어지지 않더라도 제어 한계에 가까운 진동이나 접촉 패턴을 보일 수 있으므로 안정성은 동적으로 평가해야 한다.

전도율(Fall Rate)은 심각한 이동 실패를 직접적으로 나타내는 시스템 수준 지표(System-Level Metric)이다. 하나의 성공적인 시연 결과가 아니라 지형, 속도, 외란 조건에 걸친 반복 시험에서 전도율을 보고해야 한다. 전도(Fall)의 정의도 명확해야 하며 몸체의 지면 접촉, 자세 임계값 위반, 복구할 수 없는 지지력 상실 또는 보호 정지(Protective Shutdown)의 작동 등을 포함할 수 있다. 전도 사이의 이동 시간이나 이동 거리를 함께 측정하면 추가적인 신뢰성 정보를 얻을 수 있다.

발 접촉 동작(Foot Contact Behavior)은 이동 품질을 평가하는 중요한 근거를 제공한다. 의도하지 않은 발 미끄러짐(Foot Slip), 조기 접촉(Premature Contact), 접촉 실패(Missed Contact), 입각 지속시간(Stance Duration), 유각 간극(Swing Clearance), 접촉 타이밍(Contact Timing), 충격 속도(Impact Velocity) 등을 평가할 수 있다. 과도한 미끄러짐은 궤적 정확도를 저하시키고 상태 추정을 불안정하게 만들 수 있으며, 강한 충격은 기계적 스트레스를 증가시킨다. 따라서 접촉 지표는 정책 동작을 동적 안정성과 장기적인 하드웨어 신뢰성에 연결한다.

휴머노이드 이동(Humanoid Locomotion)의 균형 관련 측정에는 질량중심(Center of Mass)의 거동, 지지 다각형(Support Polygon)과의 관계, 포획점(Capture Point) 거동, 운동량 조절(Momentum Regulation), 발 배치 일관성(Foot-Placement Consistency) 등이 포함될 수 있다. 사족보행 로봇에서는 보행 규칙성(Gait Regularity), 지지 전환(Support Transition), 듀티 팩터(Duty Factor), 다리 사이의 협응을 추가로 평가할 수 있다. 선택하는 지표는 모든 플랫폼에 하나의 보편적인 안정성 점수를 강제하기보다 로봇 형태(Morphology)와 제어기 구조(Controller Architecture)에 맞추어야 한다.

속도와 안정성은 속도가 증가할수록 균형 제어의 난이도가 변화하므로 항상 함께 분석해야 한다. 정책이 매우 높은 최대 속도를 달성하더라도 몸체 진동 증가, 미끄러짐 증가, 높은 충격 하중, 빈번한 전도를 경험할 수 있다. 따라서 다양한 명령 속도 범위에서 성능 프로파일(Performance Profile)을 생성하고 가장 빠르게 성공한 단일 시험만 보고하기보다 이동이 안정적이고 제어 가능하며 반복 가능한 운영 영역(Operating Region)을 식별해야 한다.

의미 있는 이동 평가를 위해서는 지형 다양성(Terrain Diversity)이 필수적이다. 평탄한 표면을 기준 조건으로 사용하고 실제 응용 목적에 따라 경사면, 계단, 불규칙 지형, 디딤돌 형태의 표면, 순응성 지면(Compliant Ground), 저마찰 영역 또는 장애물을 단계적으로 도입해야 한다. 동일한 속도와 안정성 값이라도 실험실 바닥에서 측정했는지 불규칙한 야외 지형에서 측정했는지에 따라 정책 능력의 의미가 크게 달라지므로 지형 특성을 명확하게 기록해야 한다.

외란 강건성(Disturbance Robustness)은 예상하지 못한 물리적 사건 이후에도 정책이 이동을 유지하거나 복구할 수 있는지를 평가한다. 외부 밀기(External Push), 적재물 변화, 일시적인 발 미끄러짐, 지형 높이 오차, 센서 외란 또는 액추에이터 변화 등을 통제된 조건에서 적용할 수 있다. 평가에서는 로봇이 균형을 유지하는지, 상태가 정상 움직임에서 얼마나 벗어나는지, 얼마나 빠르게 복구하는지, 그리고 복구 과정에서 위험한 접촉이나 과도한 관절 하중이 발생하는지를 측정해야 한다.

명령 전환 시험(Command-Transition Testing)은 실용적인 이동 작업을 수행해야 하는 정책에서 중요하다. 로봇은 출발, 정지, 가속, 회전, 후진, 그리고 지원되는 경우 걷기와 다른 보행 모드(Gait Mode) 사이를 전환하는 과정에서 평가해야 한다. 접촉 일정(Contact Schedule)과 운동량이 빠르게 변화해야 하므로 이러한 전환 과정에서는 정상상태 이동에서 나타나지 않는 불안정성이 드러날 수 있다. 성공적인 전환율(Transition Success Rate)과 안정화 시간(Stabilization Time)은 정책의 응답성을 평가하는 유용한 지표이다.

속도가 증가하면 액추에이터 구동에 필요한 에너지가 불균형적으로 증가할 수 있으므로 에너지 효율(Energy Efficiency)을 속도와 함께 측정해야 한다. 표준화된 경로에서 전력(Electrical Power), 기계적 일(Mechanical Work), 관절 토크(Joint Torque), 배터리 소비량, 수송 비용(Cost of Transport)을 기록할 수 있다. 약간 더 높은 속도를 얻기 위해 훨씬 많은 에너지를 소비하는 정책은 이동형 로봇의 실제 배치에 적합하지 않을 수 있다. 효율성 분석은 불필요한 관절 움직임과 기계적 스트레스가 큰 보행 패턴을 발견하는 데에도 도움이 된다.

이동 성능을 신뢰성 있게 특성화하려면 반복 시험(Repeated Trial)이 필요하다. 초기 자세, 지면 접촉, 센서 잡음, 액추에이터 온도, 배터리 상태, 확률적 정책 출력(Stochastic Policy Output)은 동일한 실험에서도 결과를 변화시킬 수 있다. 따라서 평균 속도나 안정성 값뿐 아니라 결과 분포, 분산(Variance), 신뢰구간(Confidence Interval), 최악 조건 동작(Worst-Case Behavior)을 함께 보고해야 한다. 특히 정책 버전 사이의 성능 향상이 통계적으로 의미 있는지를 판단하려면 반복성(Repeatability)이 중요하다.

일반화 평가(Generalization Evaluation)는 학습 과정에서 사용된 조건과 다른 환경을 대상으로 수행해야 한다. 이전에 보지 못한 지형 형상, 서로 다른 마찰계수(Friction Coefficient), 변경된 적재물, 변화된 질량 분포, 새로운 발 접촉 특성, 센서 성능 저하 등을 통해 정책이 학습 조건에 얼마나 의존하는지를 확인할 수 있다. 분포 내(In-Distribution) 조건과 분포 외(Out-of-Distribution, OOD) 조건의 성능을 비교하면 이동 능력이 익숙한 시뮬레이션 조건에만 특화된 것이 아니라 현실적인 환경 변화에도 전이되는지를 평가할 수 있다.

시뮬레이션(Simulation)은 통제된 지형 무작위화(Terrain Randomization), 외란, 동역학 변화, 반복 시험을 이용하여 대규모 이동 평가를 가능하게 한다. 그러나 실제 로봇에는 액추에이터 대역폭 제한, 백래시(Backlash), 구조적 순응성(Structural Compliance), 불완전한 마찰 모델, 센서 지연, 열적 영향(Thermal Effect), 모델링되지 않은 접촉 동역학이 존재한다. 따라서 시뮬레이션 결과를 실제 하드웨어 측정값과 비교하고 시뮬레이션-현실 전이(Simulation-to-Reality Transfer) 과정에서 발생하는 성능 저하를 정량화해야 한다.

성능 평가 중에도 안전 제약(Safety Constraint)은 항상 활성화되어 있어야 한다. 관절 위치, 속도, 토크, 모터 온도, 접촉력, 몸체 자세, 작업공간 한계(Workspace Limit)를 모니터링하여 정책이 허용 가능한 하드웨어 또는 안전 한계를 초과하면서 높은 속도 결과를 얻지 못하도록 해야 한다. 비상 정지(Emergency Stop), 보호 제어기 개입(Protective Controller Intervention), 토크 포화(Torque Saturation), 열 제한(Thermal Limiting)도 기록해야 한다. 이러한 사건은 일반적인 이동 지표만으로는 확인하기 어려운 위험한 운영 영역을 보여준다.

정책 추론과 제어는 엄격한 시간 요구조건을 만족해야 하므로 실행시간 성능(Runtime Performance)도 이동 품질에 영향을 준다. 평가에서는 실제 하드웨어에서 추론 지연시간(Inference Latency), 제어 주파수(Control Frequency), 타이밍 지터(Timing Jitter), 데드라인 누락(Missed Deadline), 프로세서 사용률, 가속기 부하(Accelerator Load), 메모리 소비량을 측정해야 한다. 정책 출력이 지연되면 이상적인 계산 환경에서는 효과적으로 보이는 동일한 정책이라도 접촉 타이밍에 위상 오차(Phase Error)를 발생시키거나 고속 움직임을 불안정하게 만들 수 있다.

완전한 평가 기록(Evaluation Record)에는 정책 버전, 로봇 구성, 지형 설명, 명령 프로파일(Command Profile), 제어 주파수, 센서 구성, 적재물, 무작위화 설정, 환경 조건, 종료 기준(Termination Criteria)을 보존해야 한다. 또한 관절 상태, 베이스 움직임, 발 접촉, 액추에이터 명령, 전력 측정값, 안전 이벤트, 실패 원인을 기록해야 한다. 이러한 기록은 회귀 분석(Regression Analysis)을 지원하고 속도 또는 안정성 변화가 특정 정책이나 시스템 변경과 어떠한 관계가 있는지 추적할 수 있게 한다.

궁극적으로 이동 정책 평가(Locomotion Policy Evaluation)는 로봇이 안정적이고 제어 가능하며 효율적이고 안전한 상태를 유지하면서 빠르게 이동할 수 있는 운영 영역(Operating Envelope)을 확립해야 한다. 속도(Speed)는 이동성과 명령 추종 능력을 나타내며, 안정성(Stability)은 현실적인 접촉과 외란 조건에서 이러한 움직임을 지속할 수 있는지를 보여준다. 지형, 강건성, 에너지, 안전성, 일반화, 실행시간 측정과 이러한 지표를 결합하면 실제 현장 배치(Field Deployment) 이전에 이동 정책을 검증하기 위한 실용적인 기반을 구축할 수 있다.

## 06.06. VLA Model Evaluation Task Generalization [w/Code]

![](images/image6.png){width="7.268055555555556in" height="7.268055555555556in"}

비전-언어-행동 모델 평가(Vision-Language-Action Model Evaluation)는 로봇이 시각적 관측(Visual Observation)과 언어 명령(Language Instruction)을 다양한 조건에서 물리적 작업을 수행하는 행동으로 변환할 수 있는지를 판단한다. 하나의 고정된 행동을 위해 학습된 정책과 달리 비전-언어-행동(VLA) 모델은 의미론적 이해(Semantic Understanding)를 체화된 실행(Embodied Execution)과 연결할 수 있어야 한다. 따라서 평가에서는 작업 성공 여부뿐 아니라 명령, 객체, 장면, 작업 변화, 상호작용 이력 전반에서 능력이 일반화되는지를 측정해야 한다.

작업 성공률(Task Success Rate)은 사전에 정의된 완료 기준(Completion Criteria)을 만족한 에피소드의 비율을 기록함으로써 VLA 성능을 평가하는 기본적인 지표를 제공한다. 완료 기준에는 요구되는 객체 상태(Object State), 로봇 상태(Robot State), 공간적 관계(Spatial Relationship), 행동 순서(Action Sequence), 종료 조건(Termination Condition)이 포함되어야 한다. 언어 명령에는 여러 가지 유효한 수행 전략이 존재할 수 있으므로 하나의 기준 궤적(Reference Trajectory)을 그대로 재현하도록 요구하기보다 요청된 물리적 결과가 실제로 달성되었는지를 중심으로 평가해야 한다.

작업 일반화(Task Generalization)는 학습 작업에서 획득한 능력이 관련성이 있지만 이전에 경험하지 못한 새로운 작업으로 전이되는지를 측정한다. 예를 들어 객체를 용기에 넣도록 학습된 로봇은 새로운 객체-용기 조합, 변경된 공간 관계, 요청된 작업의 변형을 대상으로 평가해야 한다. 평가에서는 기억된 작업 실행(Memorized Task Execution)과 익숙한 개념 및 운동 기술을 새로운 방식으로 재조합하여 새로운 명령을 수행하는 구성적 행동(Compositional Behavior)을 구분해야 한다.

명령 일반화(Instruction Generalization)는 모델이 동일하거나 관련된 목표를 나타내는 서로 다른 언어 표현을 이해할 수 있는지를 평가한다. 테스트에서는 의도된 작업을 유지하면서 어휘, 문장 구조, 지시 표현(Referring Expression), 명령 길이, 추상화 수준(Level of Abstraction)을 변화시킬 수 있다. 강건한 VLA 모델은 하나의 정형화된 명령 템플릿(Canonical Command Template)에 의존해서는 안 된다. 다양한 바꿔쓰기(Paraphrase)에 대한 성능은 언어 표현이 표면적인 문구 패턴이 아니라 작업의 의미를 실제로 포착하고 있는지를 보여준다.

객체 일반화(Object Generalization)는 학습 분포(Training Distribution)에 존재하지 않았던 객체 인스턴스(Object Instance)에 대한 조작 또는 상호작용 능력을 평가한다. 새로운 객체는 형상, 텍스처, 색상, 크기, 재질, 방향 또는 기능적 특성이 달라질 수 있다. 평가는 모델이 전이 가능한 시각적·의미론적 특징(Transferable Visual and Semantic Features)을 이용하여 적절한 행동을 선택하는지를 판단해야 한다. 알려진 범주의 새로운 인스턴스와 완전히 새로운 범주의 객체는 서로 다른 수준의 일반화 난이도를 나타내므로 결과를 구분하여 평가해야 한다.

장면 일반화(Scene Generalization)는 환경 배치가 학습 과정에서 경험한 것과 달라졌을 때에도 VLA 모델이 작업 성능을 유지하는지를 측정한다. 가구 위치, 배경, 조명, 혼잡도, 카메라 시점, 작업공간 형상(Workspace Geometry), 방해 객체(Distractor Object)를 체계적으로 변화시킬 수 있다. 높은 장면 일반화 성능은 정책이 고정된 시각적 구성이나 기억된 작업공간 위치에 의존하지 않고 명령을 관련 객체 및 공간적 관계와 연결하고 있음을 의미한다.

구성적 일반화(Compositional Generalization)는 범용 로봇 정책(Generalist Robot Policy)에서 특히 중요하다. 모델이 학습 과정에서 열기(Open), 서랍(Drawer), 빨간 객체(Red Object), 배치하기(Place)와 같은 개별 개념을 경험했더라도 새로운 작업에서 요구되는 정확한 조합은 경험하지 않았을 수 있다. 평가에서는 알려진 개념과 기술의 새로운 조합을 구성하여 모델이 인식, 언어 이해, 행동 지식을 결합하고 학습 과정에서 명시적으로 시연되지 않았던 행동을 생성할 수 있는지를 판단해야 한다.

일반화 난이도(Generalization Difficulty)는 명확하게 정의된 평가 수준(Evaluation Level)으로 구성해야 한다. 분포 내 테스트(In-Distribution Test)는 익숙한 작업 구조와 환경 조건을 사용하여 기준 성능(Baseline Capability)을 확립한다. 경미한 분포 변화(Distribution Shift)에서는 새로운 객체 인스턴스나 명령 바꿔쓰기를 도입할 수 있으며, 더 강한 분포 변화에서는 새로운 장면, 객체, 목표, 언어 표현을 동시에 결합할 수 있다. 각 수준의 결과를 별도로 보고하면 작업이 학습 분포에서 멀어질수록 발생하는 급격한 성능 저하가 종합 성공률에 가려지는 것을 방지할 수 있다.

장기 작업(Long-Horizon Task)은 개별 행동이 올바르게 보이더라도 누적된 오류로 인해 전체 작업이 실패할 수 있으므로 추가적인 평가가 필요하다. VLA 모델은 객체를 찾고, 접근하고, 파지하고, 용기를 열고, 객체를 배치한 다음 완료 여부를 확인해야 할 수 있다. 평가자는 전체 작업 성공(Complete Task Success)과 하위 작업 완료(Subtask Completion)를 모두 기록해야 한다. 이를 통해 실패가 의미론적 이해 오류, 인식, 행동 실행, 순서 결정(Sequencing), 복구 또는 작업 맥락(Task Context)의 손실 중 어디에서 발생했는지를 파악할 수 있다.

명령 수행 정확도(Instruction-Following Accuracy)는 로봇이 단순히 물리적으로 성공한 행동을 수행했는지가 아니라 실제로 요청된 작업을 수행했는지를 평가해야 한다. 병을 옮기라는 명령을 받았음에도 근처의 컵을 집었다면 조작 자체는 성공했더라도 명령 수행에는 실패한 것이다. 따라서 평가에서는 객체 식별, 속성(Attribute), 공간 관계, 목적지, 작업 순서 요구사항, 명시된 금지 행동(Prohibited Action) 등 명령에 포함된 의미론적 제약(Semantic Constraint)과 실제 수행 행동을 비교해야 한다.

모호한 명령(Ambiguous Instruction)은 VLA 동작을 평가하는 또 다른 중요한 시험 요소이다. 실제 사용자는 불완전한 지시 대상, 충분히 구체적이지 않은 목표, 여러 가지로 해석할 수 있는 명령을 제공할 수 있다. 평가는 모델이 보수적으로 행동하는지, 지원되는 경우 명확화 요청(Clarification Request)을 수행하는지, 또는 사용 가능한 맥락을 기반으로 적절한 해석을 선택하는지를 판단해야 한다. 사람과 상호작용하는 로봇 시스템에서는 근거가 부족한 해석을 높은 확신으로 실행하는 것이 불확실성을 명시적으로 인식하는 것보다 더 큰 문제가 될 수 있다.

강건성 시험(Robustness Testing)에서는 시각적, 언어적, 물리적 교란(Perturbation)을 동시에 도입해야 한다. 하나의 작업 과정에서 가림(Occlusion), 조명 변화, 센서 잡음, 객체 이동, 불완전한 파지, 명령 바꿔쓰기, 예상하지 못한 환경 변화가 함께 발생할 수 있다. 우수한 VLA 모델은 오래된 관측에서 생성한 행동 순서를 맹목적으로 실행하기보다 현재의 물리적 상태에 언어를 지속적으로 연결하고 조건이 변화하면 행동을 수정할 수 있어야 한다.

복구 능력(Recovery Capability)은 범용 물리 작업이 예상대로 정확하게 진행되는 경우가 드물기 때문에 중요하다. 객체가 미끄러지거나, 서랍이 열리지 않거나, 파지 시도가 실패하거나, 다른 행위자(Agent)가 장면을 변경할 수 있다. 평가에서는 VLA 모델이 행동 실패 결과를 감지하고 환경에 대한 이해를 갱신하며 수정 행동(Corrective Action)을 선택하는지를 측정해야 한다. 복구 성공률, 재시도 횟수, 추가 실행시간, 반복적인 실패 루프(Failure Loop)는 정책의 적응성을 평가하는 유용한 근거가 된다.

안전성 평가(Safety Evaluation)는 작업 성공과 독립적으로 유지되어야 한다. VLA 모델이 위험한 움직임, 과도한 접촉, 충돌, 불안정한 파지 또는 작업공간 제약을 위반하는 행동을 통해 명령을 완료했다면 우수한 평가를 받아서는 안 된다. 테스트에는 현재 장면의 상태로 인해 명령 수행이 위험해지는 상황과 의미론적 목표가 물리적 한계와 충돌하는 상황을 포함해야 한다. 안전한 거부(Safe Refusal), 재계획(Replanning), 작업 종료(Termination)는 요청된 작업이 완료되지 않더라도 올바른 행동으로 평가될 수 있다.

명령 해석이나 행동의 적절성을 수치적으로 표현하기 어려운 경우 인간 평가(Human Evaluation)를 자동화된 지표와 함께 사용할 수 있다. 평가자는 로봇의 행동이 명령의 의도와 일치하는지, 행동을 예측할 수 있는지, 작업 수행이 적절하게 신중한지를 평가할 수 있다. 주관적인 인상이 재현 가능한 정량적 증거를 대체하지 않도록 인간 평가는 사전에 정의된 평가 기준을 사용하고 가능한 경우 여러 평가자(Multiple Evaluators)를 활용해야 한다.

시뮬레이션(Simulation)과 기록된 데이터셋(Recorded Dataset)을 사용하면 다양한 작업 조합에 걸쳐 광범위한 VLA 평가를 수행할 수 있지만 행동 예측이 접촉 동역학(Contact Dynamics), 센싱 오류, 실제 객체와 상호작용하므로 물리적 검증(Physical Validation)이 필요하다. 효과적인 평가 과정은 오프라인 행동 또는 궤적 평가(Offline Action or Trajectory Assessment)에서 시작하여 상호작용형 시뮬레이션(Interactive Simulation), 통제된 실제 로봇 실험으로 발전한다. 각 단계의 성능 차이를 분석하면 우수해 보이는 의미론적 능력이 실제 체화된 행동으로 안정적으로 연결되지 않는 지점을 확인할 수 있다.

대규모 VLA 모델(Large VLA Model)은 다중모달 추론(Multimodal Inference) 과정에서 상당한 지연시간을 발생시킬 수 있으므로 실행시간 성능(Runtime Performance)이 특히 중요하다. 평가는 실제 배치 하드웨어에서 관측-행동 지연시간(Observation-to-Action Delay), 행동 생성 주파수(Action Generation Frequency), 메모리 사용량, 가속기 활용률(Accelerator Utilization), 타이밍 변동성(Timing Variability)을 측정해야 한다. 추론 시간이 지나치게 길어지면 행동을 실행하기 전에 환경 상태가 변화할 수 있으므로 동적인 물리 환경에서는 정확한 예측이라도 실질적인 가치가 감소할 수 있다.

완전한 VLA 평가 기록(Evaluation Record)에는 모델 버전, 학습 데이터 경계(Training-Data Boundary), 작업 정의, 명령 텍스트, 객체 및 장면 식별자, 로봇 신체 구조(Robot Embodiment), 초기 조건, 성공 기준, 무작위화 설정(Randomization Setting)을 보존해야 한다. 또한 센서 관측, 생성된 행동, 궤적, 작업 상태 전환(Task-State Transition), 개입(Intervention), 실패, 타이밍 데이터를 기록해야 한다. 이러한 기록은 작업 일반화 결과를 재현 가능하게 만들고 연속적인 모델 릴리스 사이의 회귀 분석(Regression Analysis)을 지원한다.

궁극적으로 VLA 평가(VLA Evaluation)는 모델이 특정 벤치마크에 특화된 능력(Benchmark-Specific Competence)이 아니라 전이 가능한 체화 능력(Transferable Embodied Capability)을 보유하고 있는지를 판단해야 한다. 작업 성공은 목표가 완료되었는지를 나타내며, 명령, 객체, 장면, 구성적 일반화 평가는 익숙한 조건을 넘어 능력이 어느 정도까지 확장되는지를 보여준다. 장기 작업 실행, 복구, 안전성, 강건성, 인간 평가, 실행시간 측정과 이러한 평가를 결합하면 실제 환경 배치(Real-World Deployment) 이전에 범용 로봇 정책(Generalist Robot Policy)을 판단하기 위한 실용적인 기반을 구축할 수 있다.

## 06.07. OOD Robustness Evaluation Protocol [w/Code]

![](images/image7.png){width="7.268055555555556in" height="7.268055555555556in"}

분포 외 강건성 평가(Out-of-Distribution Robustness Evaluation)는 실제 배치 조건이 학습 과정에서 표현된 조건과 달라졌을 때에도 로봇 인공지능 모델(Robotic AI Model)이 신뢰할 수 있는 동작을 지속하는지를 판단한다. 이러한 차이는 새로운 객체, 환경, 센서 특성, 날씨, 조명, 로봇 동역학(Robot Dynamics), 인간 행동 등에서 발생할 수 있다. 실제 로봇은 미래의 관측값이 항상 학습 분포(Training Distribution)를 따른다고 가정할 수 없으므로 분포 외(OOD) 평가는 선택적인 스트레스 테스트가 아니라 모델 검증(Model Validation)의 기본적인 구성요소이다.

분포 외 평가 프로토콜(OOD Evaluation Protocol)은 먼저 분포 내 기준 조건(In-Distribution Reference Condition)을 정의하는 것에서 시작해야 한다. 분포 변화(Distribution Shift)를 도입하기 전에 학습 데이터 경계(Training-Data Boundary), 검증 영역(Validation Domain), 센서 구성, 작업 정의, 환경 가정(Environmental Assumption), 로봇 신체 구조(Robot Embodiment)를 문서화해야 한다. 이러한 기준선이 없으면 어려운 테스트가 실제 분포 변화를 나타내는지, 일반적인 작업 복잡성을 의미하는지, 또는 모델 개발 과정에서 이미 포함된 조건인지를 판단하기 어렵다.

분포 변화(Distribution Shift)는 해석 가능한 범주로 구성해야 한다. 공변량 변화(Covariate Shift)는 기본 작업을 유지하면서 시각적 외형이나 센서 통계 특성을 변화시킬 수 있으며, 의미론적 변화(Semantic Shift)는 익숙하지 않은 객체, 클래스, 명령 또는 장면 개념을 도입한다. 동역학 변화(Dynamics Shift)는 마찰, 적재물, 액추에이터 동작 또는 접촉 특성을 변화시키며, 맥락 변화(Contextual Shift)는 기존에 익숙한 요소 사이의 관계를 변경한다. 이러한 범주를 구분하면 모델이 어떤 가정에 가장 강하게 의존하는지 파악할 수 있다.

분포 외 심각도(OOD Severity)는 하나의 극단적인 테스트로 표현하기보다 점진적으로 변화시켜야 한다. 경미한 변화에는 중간 수준의 조명 변화, 작은 센서 잡음 또는 알려진 객체 범주의 익숙하지 않은 인스턴스가 포함될 수 있다. 더 강한 변화에서는 새로운 환경, 심각한 가림(Occlusion), 변화된 동역학, 익숙하지 않은 의미론적 범주 또는 여러 외란의 조합을 도입할 수 있다. 이러한 심각도 단계(Severity Ladder)는 운영 조건이 학습 분포에서 멀어질수록 성능이 얼마나 점진적으로 저하되는지를 보여준다.

기준 평가(Baseline Evaluation)는 먼저 대표적인 분포 내 조건에서 성능을 확립해야 하며, 이후 분포 외 테스트에서도 동일한 작업 정의와 평가 지표를 사용해야 한다. 모델 유형에 따라 이러한 지표에는 탐지 정확도(Detection Accuracy), 작업 성공률(Task Success), 내비게이션 효율성(Navigation Efficiency), 조작 성공률(Manipulation Success), 이동 안정성(Locomotion Stability), 명령 수행 정확도(Instruction-Following Accuracy) 등이 포함될 수 있다. 이후 분포 외 강건성은 절대 성능과 설정된 기준선 대비 성능 저하량으로 표현할 수 있다.

단일 요인 시험(Single-Factor Testing)은 다른 조건을 가능한 일정하게 유지하면서 하나의 분포 변화만 분리하여 평가한다. 예를 들어 인식 모델(Perception Model)은 장면의 기하학적 구조를 고정한 상태에서 다양한 조명 수준에 대해 평가할 수 있으며, 조작 정책(Manipulation Policy)은 객체 형상과 자세를 유지하면서 서로 다른 객체 질량을 대상으로 시험할 수 있다. 이러한 접근법은 관찰된 성능 저하를 통제되지 않은 여러 환경 변화가 아니라 특정 요인과 연관시킬 수 있으므로 명확한 진단 정보를 제공한다.

다중 요인 시험(Multi-Factor Testing)은 실제 배치 환경에서 분포 변화가 독립적으로 발생하는 경우가 드물기 때문에 필요하다. 어두운 환경은 비, 센서 오염, 익숙하지 않은 장애물, 낮은 마찰력과 동시에 발생할 수 있으며, 조작 작업에서는 새로운 객체와 혼잡한 환경 및 변경된 카메라 시점이 함께 나타날 수 있다. 따라서 개별 요인의 특성을 먼저 평가한 후 통제된 분포 변화의 조합을 시험하여 요인 간 상호작용 효과(Interaction Effect)와 복합적인 실패(Compounded Failure)를 확인해야 한다.

분포 외 데이터셋(OOD Dataset)과 시나리오는 학습 및 모델 선택(Model Selection) 과정과 분리되어야 한다. 보지 못한 평가 세트라고 정의한 데이터에 대해 반복적으로 모델을 조정하면 해당 데이터는 점차 개발 분포(Development Distribution)의 일부가 된다. 가능한 경우 프로토콜은 숨겨진 또는 고정된 테스트 시나리오(Hidden or Frozen Test Scenario)를 유지하고 데이터셋 버전을 추적해야 한다. 또한 평가 데이터가 모델 선택, 임계값 조정, 프롬프트 설계(Prompt Design), 미세조정(Fine-Tuning), 정책 개발에 영향을 주었는지를 문서화해야 한다.

강건성 평가(Robustness Evaluation)는 평균적인 작업 성능만 측정해서는 안 된다. 평균 결과는 물리적 시스템에서 특히 중요한 드물지만 치명적인 실패(Catastrophic Failure)를 감출 수 있다. 평가 보고서에는 결과 분포, 백분위수(Percentile), 분산(Variance), 최악 조건 결과(Worst-Case Outcome), 실패율, 분포 외 범주 및 심각도별 성능을 포함해야 한다. 정책의 확률성, 센서 잡음, 접촉 동역학, 환경 변화로 인해 명목상 동일한 조건에서도 결과가 달라질 수 있는 경우 반복 시험(Repeated Trial)이 필요하다.

불확실성 동작(Uncertainty Behavior)은 작업 성능과 함께 평가해야 한다. 익숙하지 않은 입력을 접한 모델은 높은 신뢰도로 잘못된 예측을 생성하기보다 이상적으로는 신뢰도를 낮추거나 다른 방식으로 불확실성을 표현해야 한다. 평가는 분포 외 심각도가 증가함에 따라 예측 신뢰도와 실제 정확성 사이의 관계를 비교할 수 있으며, 불확실성 추정(Uncertainty Estimation)이 거부 판단(Rejection), 폴백 제어(Fallback Control), 중복 센싱(Redundant Sensing), 인간 개입(Human Intervention), 보수적 계획(Conservative Planning)에 유용한 신호를 제공하는지 확인할 수 있다.

분포 외 탐지 능력(OOD Detection Capability)은 강건성과 별도로 평가할 수 있다. 모델은 관련 작업을 완료하지 못하더라도 입력이 익숙하지 않다는 사실을 인식할 수 있으며, 반대로 다른 모델은 분포 변화를 명시적으로 탐지하지 않으면서도 중간 수준의 변화에서 비교적 양호한 성능을 유지할 수 있다. 따라서 탐지 시험에서는 분포 내 샘플과 분포 외 샘플의 판별 능력, 임계값 민감도(Threshold Sensitivity), 오경보(False Alarm), 탐지되지 않은 OOD 이벤트, 그리고 로봇 동작에 영향을 줄 수 있을 만큼 충분히 빠르게 탐지되는지를 평가해야 한다.

모델이 자신의 능력 범위(Competence Boundary)를 벗어나 동작할 때의 실패 행동(Failure Behavior)은 특히 중요하다. 프로토콜에서는 성능 저하가 점진적(Graceful)인지 급격한지를 평가하고, 신뢰도 또는 작업 성능이 불안정해질 때 로봇이 안전 상태(Safe State)로 전환하는지를 확인해야 한다. 물리적 시스템에서는 불확실한 행동을 계속하여 충돌이나 조작 위험을 증가시키는 것보다 제어된 감속, 정지, 지원 요청 또는 보수적인 폴백 정책(Conservative Fallback Policy)으로 전환하는 것이 더 적절할 수 있다.

분포 변화는 운영 과정에서 점진적으로 나타날 수도 있으므로 시간적 분포 외 조건(Temporal OOD Condition)도 포함해야 한다. 조명은 수 시간에 걸쳐 변화할 수 있고, 센서 오염은 점진적으로 누적될 수 있으며, 위치 추정 드리프트(Localization Drift)가 증가하거나 액추에이터 온도가 시스템 동역학을 변화시킬 수 있다. 시퀀스 기반 평가(Sequence-Based Evaluation)는 모델이 점진적인 성능 저하를 감지하고 적절하게 적응하는지, 그리고 개별 프레임이나 짧은 에피소드 평가에서는 발견하기 어려운 불안정한 전환을 방지하는지를 판단해야 한다.

교차 센서 강건성(Cross-Sensor Robustness)은 카메라, 라이다(LiDAR), 깊이 센서(Depth Sensor), 관성측정장치(IMU), 촉각 센서(Tactile Sensor), 다중모달 융합(Multimodal Fusion)에 의존하는 모델에서 중요하다. 테스트에서는 보정 오차(Calibration Error), 잡음 변화, 측정값 누락, 부분적인 센서 고장 또는 센서 모달리티 간 불일치(Disagreement Between Modalities)를 도입할 수 있다. 평가는 모델이 중복 정보를 활용하여 기능을 유지하는지, 서로 일치하지 않는 입력을 인식하는지, 또는 하나의 센싱 채널이 예상 분포를 벗어났을 때 이를 인식하지 못한 채 실패하는지를 판단해야 한다.

시뮬레이션(Simulation)은 실제 환경에서 구현하기에 비용이 많이 들거나 위험하거나 반복 재현하기 어려운 분포 외 변화를 체계적으로 생성하는 데 유용하다. 도메인 무작위화(Domain Randomization)를 통해 수천 번의 시험에서 조명, 텍스처, 객체 형상, 지형, 마찰, 센서 잡음, 동역학을 변화시킬 수 있다. 그러나 시뮬레이션으로 생성된 OOD 조건이 모든 실제 분포 변화를 대표한다고 가정해서는 안 된다. 시뮬레이션에서 관찰된 강건성이 실제 센서, 접촉, 환경 외란에서도 유지되는지를 확인하기 위해 물리적 실험(Physical Experiment)이 필요하다.

현장에서 수집된 분포 외 시나리오(Field-Derived OOD Scenario)는 설계자가 예상하지 못했던 가정을 드러낼 수 있으므로 특히 중요한 평가 근거를 제공한다. 예상하지 못한 객체, 비정상적인 인간 행동, 날씨 영향, 반사 표면(Reflective Surface), 건설 환경 변화, 센서 오염, 운영상의 오용(Operational Misuse)은 이전에 알려지지 않았던 실패 모드(Failure Mode)를 드러낼 수 있다. 이러한 사건을 분류하고 재현 가능한 회귀 시나리오(Regression Scenario)로 변환하면 실제 현장 경험을 기반으로 평가 스위트(Evaluation Suite)를 지속적으로 강화할 수 있다.

안전 중요 분포 외 시험(Safety-Critical OOD Testing)은 발생 확률이 낮더라도 실패 결과가 심각한 분포 변화를 우선적으로 평가해야 한다. 사람 탐지 실패, 익숙하지 않은 지형에서의 불안정한 이동, 사람 근처에서의 잘못된 조작, 제한된 공간에서의 내비게이션 실패 등이 대표적인 사례이다. 위험 기반 우선순위화(Risk-Based Prioritization)는 노출 가능성(Exposure Likelihood), 모델 민감도(Model Sensitivity), 결과의 심각도(Consequence Severity)를 결합하여 실제 배치 전에 어떤 OOD 시나리오에 가장 강력한 평가 증거가 필요한지를 결정할 수 있다.

익숙하지 않은 입력은 계산 요구량에도 영향을 줄 수 있으므로 실행시간 동작(Runtime Behavior)은 분포 외 평가의 일부로 유지해야 한다. 더 많은 탐지 객체, 긴 입력 시퀀스, 복잡한 장면 또는 추가적인 복구 추론(Recovery Reasoning)은 추론 지연시간(Inference Latency), 메모리 소비량, 가속기 활용률(Accelerator Utilization)을 증가시킬 수 있다. 프로토콜은 다양한 분포 변화에서 타이밍과 자원 사용량을 측정하여 모델이 통계적 정확성을 유지하면서 어려운 조건에서 실시간 제약(Real-Time Constraint)을 위반하는 상황이 발생하지 않는지를 확인해야 한다.

완전한 분포 외 평가 기록(OOD Evaluation Record)에는 모델 버전, 학습 데이터 경계, 시나리오 정의, 분포 변화 범주, 심각도 수준, 난수 시드(Random Seed), 센서 구성, 로봇 상태, 환경 매개변수, 평가 지표, 종료 기준(Termination Criteria)을 보존해야 한다. 가능한 경우 원시 관측 데이터(Raw Observation), 모델 출력, 신뢰도 값, 행동, 안전 시스템 개입(Safety Intervention), 실패 원인도 함께 기록해야 한다. 이러한 기록은 모델과 실제 배치 환경이 변화함에 따라 재현 가능한 회귀 테스트(Regression Testing)를 수행할 수 있도록 한다.

궁극적으로 분포 외 강건성 평가 프로토콜(OOD Robustness Evaluation Protocol)은 로봇 인공지능 모델이 익숙한 운영 분포(Familiar Operating Distribution)를 어느 정도까지 벗어나도 신뢰할 수 있는 성능을 유지하는지, 그리고 그 한계에 도달했을 때 얼마나 안전하게 행동하는지를 확립해야 한다. 통제된 분포 변화, 심각도 단계, 불확실성 분석, 실패 특성화(Failure Characterization), 시뮬레이션, 물리적 시험, 현장 기반 회귀 사례를 결합함으로써 방어 가능한 배치 운영 범위(Deployment Envelope)와 폴백 전략(Fallback Strategy)을 정의하기 위한 체계적인 근거를 제공할 수 있다.

## 06.08. AI Inference Latency and Energy Benchmark [w/Code]

![](images/image8.png){width="7.268055555555556in" height="7.268055555555556in"}

AI 추론 지연시간 및 에너지 벤치마킹(AI Inference Latency and Energy Benchmarking)은 로봇 AI 모델(Robotic AI Model)이 목표 플랫폼의 시간 및 전력 제약 내에서 실행될 수 있는지를 판단한다. 인식(Perception), 내비게이션(Navigation), 조작(Manipulation), 이동(Locomotion), 비전-언어-행동(VLA) 추론이 물리적 제어 루프(Physical Control Loop)에 참여해야 하는 경우 모델 정확도만으로는 충분하지 않다. 따라서 벤치마킹에서는 대표적인 실제 배치 조건에서 응답시간, 처리량(Throughput), 타이밍 변동성(Timing Variability), 연산 자원 활용률, 전력 소비량, 추론당 에너지(Energy per Inference)를 평가해야 한다.

추론 지연시간(Inference Latency)은 명확한 측정 경계(Measurement Boundary)를 사용하여 정의해야 한다. 응용 분야에 따라 지연시간은 모델 실행 시간만을 의미할 수도 있고, 전처리부터 출력까지의 시간, 센서 입력부터 예측까지의 지연 또는 전체 관측-행동 간격(Observation-to-Action Interval)을 의미할 수도 있다. 영상 디코딩, 텐서 변환(Tensor Conversion), 메모리 전송, 후처리(Postprocessing), 미들웨어 통신(Middleware Communication), 행동 생성(Action Generation)이 신경망 순전파(Neural-Network Forward Pass) 외부에서 상당한 시간을 소비할 수 있으므로 이러한 값은 크게 달라질 수 있다. 따라서 벤치마크에서는 시간 측정의 시작점과 종료점을 정확하게 명시해야 한다.

지연시간 분포(Latency Distribution)는 평균 지연시간 하나만 사용하는 것보다 더 많은 정보를 제공한다. 평균 성능이 허용 가능한 수준으로 보이더라도 간헐적으로 발생하는 긴 추론 지연이 로봇의 실시간 동작에 영향을 줄 수 있다. 따라서 벤치마크에서는 중앙값 지연시간과 함께 P95 또는 P99와 같은 상위 백분위수(Percentile), 관측된 최대 지연시간, 필요한 경우 타이밍 지터(Timing Jitter)를 보고해야 한다. 꼬리 지연시간(Tail Latency)은 드물게 발생하는 데드라인 위반(Deadline Violation)이 정상적으로 신뢰성 있게 동작하는 시스템을 불안정하게 만들 수 있으므로 안전 중요 시스템이나 고주파 제어 루프에서 특히 중요하다.

워밍업 동작(Warm-Up Behavior)은 정상상태 추론(Steady-State Inference)과 구분해야 한다. 초기 실행에는 모델 로딩(Model Loading), 메모리 할당, 그래프 컴파일(Graph Compilation), 커널 초기화(Kernel Initialization), 캐시 채우기(Cache Population), 가속기 주파수 변경 등이 포함될 수 있으며 이후의 추론 주기에서는 이러한 과정이 반복되지 않을 수 있다. 벤치마크에서는 워밍업 반복 횟수를 기록하고 운영상 중요한 경우 시작 지연시간(Startup Latency)을 별도로 보고해야 한다. 이는 모델을 지속적으로 메모리에 유지하지 않고 필요할 때 동적으로 활성화하는 로봇에서 특히 중요하다.

처리량(Throughput)은 단위시간 동안 처리할 수 있는 샘플, 프레임, 토큰, 궤적 또는 행동 예측의 수를 측정한다. 처리량과 지연시간은 서로 관련되어 있지만 서로 다른 운영 특성을 나타낸다. 배치 처리(Batching)는 처리량을 크게 증가시킬 수 있지만 개별 관측값이 경험하는 지연시간을 증가시킬 수 있다. 실시간 로보틱스(Real-Time Robotics)에서는 일반적으로 낮은 단일 샘플 지연시간(Single-Sample Latency)이 중요하지만 오프라인 지도 작성, 플릿 분석(Fleet Analytics), 일괄 인식(Batch Perception)에서는 최대 처리량이 더 중요할 수 있다.

벤치마크 입력 조건(Benchmark Input Condition)은 실제 배치 작업부하(Deployed Workload)를 대표해야 한다. 영상 해상도, 포인트 클라우드(Point Cloud) 크기, 시퀀스 길이, 언어 문맥 길이(Language Context Length), 탐지 객체 수, 행동 지평(Action Horizon), 배치 크기(Batch Size)는 모두 실행시간에 영향을 줄 수 있다. 이러한 매개변수를 명시하지 않은 지연시간 보고는 비교를 오도할 수 있다. 동적인 작업부하에서는 일반적인 입력뿐 아니라 어려운 입력도 포함해야 한다. 복잡한 장면이나 긴 다중모달 문맥(Multimodal Context)이 처리시간을 증가시키고 자원 병목(Resource Bottleneck)을 드러낼 수 있기 때문이다.

하드웨어 구성(Hardware Configuration)은 벤치마크 정의의 일부로 취급해야 한다. CPU 모델, GPU 또는 가속기 유형, 메모리 용량, 메모리 대역폭(Memory Bandwidth), 전력 모드(Power Mode), 클록 설정, 열 상태(Thermal State), 소프트웨어 스택(Software Stack)은 결과에 상당한 영향을 줄 수 있다. 실제 배치 결정을 위한 측정은 데스크톱이나 데이터센터 가속기의 결과를 추정하여 사용하는 것이 아니라 대표적인 엣지 하드웨어(Edge Hardware)에서 수행해야 한다. 동일한 모델이라도 플랫폼에 따라 지연시간과 효율 특성이 크게 달라질 수 있다.

수치 정밀도(Numerical Precision)와 모델 최적화(Model Optimization)도 명확하게 기록해야 한다. FP32, FP16, BF16, INT8 또는 기타 양자화 실행 모드(Quantized Execution Mode)는 지연시간, 메모리 사용량, 전력 소비량, 예측 품질을 변화시킬 수 있다. 컴파일러 최적화(Compiler Optimization), 연산자 융합(Operator Fusion), TensorRT 형태의 추론 엔진, 그래프 최적화(Graph Optimization), 가지치기(Pruning), 아키텍처 특화 커널(Architecture-Specific Kernel)도 성능을 변화시킬 수 있다. 따라서 모든 벤치마크 결과는 측정에 사용된 정확한 모델 산출물(Model Artifact)과 추론 구성(Inference Configuration)에 연결되어야 한다.

전력 측정(Power Measurement)은 추론 과정에서 발생하는 순간적인 전기적 요구량을 특성화한다. 사용 가능한 계측 방법에 따라 가속기 텔레메트리(Accelerator Telemetry), 시스템 전력 센서, 배터리 인터페이스, 외부 전력 분석기(External Power Analyzer), 전용 측정 하드웨어에서 값을 수집할 수 있다. GPU 전력만 측정한 값, 컴퓨팅 모듈 전체 전력, 로봇 시스템 전체 전력은 서로 다른 물리량을 나타내며 직접 비교해서는 안 되므로 측정 경계를 명확하게 명시해야 한다.

추론당 에너지(Energy per Inference)는 추론 결과 하나를 생성하는 데 필요한 시간 동안의 전력을 적분하여 유용한 효율성 지표를 제공한다. 순간 전력이 높은 모델이라도 매우 빠르게 처리를 완료하면 에너지 효율적일 수 있으며, 반대로 저전력 모델이라도 추론 시간이 훨씬 길다면 전체 에너지 소비량이 더 클 수 있다. 연속적인 인식 시스템에서는 운영 목표에 따라 프레임당 에너지(Energy per Frame), 처리된 센서 데이터의 초당 에너지 또는 완료된 작업당 에너지(Energy per Completed Task)를 보고할 수도 있다.

유휴 전력(Idle Power)은 추론에 의해 추가되는 전력(Incremental Inference Power)과 구분해야 한다. 엣지 컴퓨터, 센서, 네트워크 장치, 가속기는 AI 모델이 데이터를 적극적으로 처리하지 않을 때에도 에너지를 소비한다. 시스템 전체 전력만 측정하면 추론 자체로 인해 추가된 에너지 비용을 명확하게 파악하기 어렵다. 따라서 벤치마크에서는 유휴 기준 전력(Idle Baseline Power), 활성 전력(Active Power), 기준선 대비 증가한 에너지(Incremental Energy)를 보고할 수 있으며, 시스템 전체 측정값은 배터리 지속시간과 열 요구조건을 추정하는 데 여전히 중요하다.

에너지 벤치마킹(Energy Benchmarking)은 현실적인 듀티 사이클(Duty Cycle)을 반영해야 한다. 일부 인식 모델은 카메라 주파수에 맞추어 지속적으로 실행되지만 플래너(Planner)나 VLA 모델은 새로운 의사결정이 필요한 경우에만 실행될 수 있다. 최대 사용률로 지속 실행하는 벤치마크는 간헐적인 작업부하의 실제 소비량을 과대평가할 수 있으며, 짧고 분리된 측정은 지속적인 열 영향을 과소평가할 수 있다. 따라서 예상되는 추론 주파수, 유휴 간격, 작업부하 버스트(Workload Burst)를 재현하는 대표적인 실행 스케줄을 사용해야 한다.

열적 동작(Thermal Behavior)은 지연시간 및 에너지와 밀접하게 연결되어 있다. 지속적인 AI 작업부하는 가속기와 프로세서의 온도를 증가시키고 클록 감소 또는 열 스로틀링(Thermal Throttling)을 발생시켜 추론 성능을 점진적으로 변화시킬 수 있다. 연속 동작이 예상되는 경우 정상 열 상태(Steady Thermal Condition)를 관찰할 수 있을 만큼 충분한 시간 동안 벤치마크를 수행해야 한다. 시간에 따른 온도, 클록 주파수, 전력 상태, 지연시간을 측정하면 짧은 성능 시험에서는 나타나지 않는 성능 저하를 확인할 수 있다.

로봇 수준 타이밍(Robot-Level Timing)은 주변 소프트웨어 파이프라인과의 상호작용을 포함해야 한다. 센서 획득(Sensor Acquisition), ROS 2 또는 미들웨어 전송, 전처리, 모델 실행, 후처리, 계획(Planning), 액추에이터 명령 발행(Actuator Command Publication)은 각각 종단간 지연시간(End-to-End Latency)에 영향을 줄 수 있다. 모델 수준 벤치마크는 최적화에 유용하지만 시스템 검증(System Validation)에서는 센서-행동 지연시간(Sensor-to-Action Latency)도 측정해야 한다. 이 값은 로봇이 실제로 반응하는 순간 환경 정보가 얼마나 오래된 것인지를 결정하기 때문이다.

동시 실행(Concurrency)은 벤치마크 결과를 크게 변화시킬 수 있다. 실제 배치된 로봇에서는 인식, 위치 추정, 지도 작성, 계획, 로깅, 통신, 여러 AI 모델이 동일한 컴퓨팅 플랫폼에서 동시에 실행될 수 있다. 각 모델이 독립적으로 우수한 성능을 보이더라도 자원 경합(Resource Contention)으로 인해 지연시간과 에너지 소비량이 증가할 수 있다. 따라서 벤치마크에서는 독립 모델 측정과 대표적인 동시 작업부하(Concurrent Workload)를 모두 포함하여 공유 CPU, GPU, 메모리 또는 입출력 자원이 타이밍 위반을 발생시키는지를 판단해야 한다.

지연시간과 에너지는 모델 품질(Model Quality)과 함께 평가해야 한다. 양자화(Quantization), 낮은 해상도, 소형 네트워크, 짧은 문맥 윈도(Context Window), 낮은 추론 주파수는 효율성을 향상시킬 수 있지만 인식 정확도나 작업 성공률을 저하시킬 수 있다. 따라서 벤치마킹은 계산 지표만 독립적으로 최적화하지 않고 이러한 상충관계(Tradeoff)를 명확하게 보여주어야 한다. 파레토 방식 비교(Pareto-Style Comparison)를 사용하면 로봇의 운영 요구조건에 적합한 정확도, 지연시간, 에너지의 조합을 식별할 수 있다.

실시간 허용 기준(Real-Time Acceptance Criteria)은 시스템 요구사항(System Requirements)에서 도출해야 한다. 이동 제어기(Locomotion Controller)는 매우 짧은 관측-행동 지연만 허용할 수 있지만 의미론적 인식(Semantic Perception)이나 상위 수준 작업 계획(High-Level Task Planning)은 더 낮은 주파수로 동작할 수 있다. 따라서 벤치마크에서는 측정된 지연시간, 지터, 데드라인 누락 빈도(Deadline-Miss Frequency)를 각 AI 구성요소에 할당된 타이밍 예산(Timing Budget)과 비교해야 한다. 일반적인 성능 목표를 만족하는 것보다 실제 로봇 제어 구조의 요구사항을 충족하는지를 입증하는 것이 더 중요하다.

재현성(Reproducibility)을 확보하려면 통제된 벤치마크 절차가 필요하다. 모델 버전, 입력 데이터셋, 배치 크기, 수치 정밀도, 하드웨어, 운영체제 구성, 드라이버 버전, 추론 런타임(Inference Runtime), 전력 모드, 워밍업 절차, 측정 지속시간, 백그라운드 작업부하를 기록해야 한다. 성능 변동성을 특성화하기 위해 여러 번 반복 측정을 수행해야 하며, 자동화 스크립트는 원시 타이밍 및 전력 샘플을 보존하여 소프트웨어와 모델 릴리스 사이의 성능 회귀(Performance Regression)를 탐지할 수 있도록 해야 한다.

완전한 벤치마크(Complete Benchmark)는 하나의 지연시간이나 전력 수치만 제공해서는 안 된다. 유용한 결과에는 지연시간 분포, 처리량, 데드라인 위반, 메모리 사용량, 프로세서 및 가속기 활용률, 평균 및 최대 전력, 추론당 에너지, 온도, 지속 성능(Sustained Performance)이 포함된다. 이러한 측정값을 모델 정확도 또는 작업 성공률과 연계하면 특정 최적화가 하나의 독립적인 계산 지표만 향상시킨 것이 아니라 실제 배치 가능한 로봇 시스템 전체를 개선했는지를 판단할 수 있다.

궁극적으로 AI 추론 지연시간 및 에너지 벤치마킹(AI Inference Latency and Energy Benchmarking)은 모델이 로봇의 연산, 전력, 열, 타이밍 운영 범위(Operating Envelope) 내에서 유용한 지능을 제공할 수 있는지를 확립한다. 신뢰할 수 있는 평가는 명확하게 정의된 타이밍 경계, 현실적인 작업부하, 대표적인 하드웨어, 지속적인 측정, 모델 품질 지표를 결합해야 한다. 이러한 평가 근거는 모델 선택, 엣지 컴퓨팅 용량 산정(Edge-Compute Sizing), 배터리 계획, 열 설계(Thermal Design), 회귀 테스트, 로봇 AI 시스템의 안전한 실시간 배치(Real-Time Deployment)를 지원한다.

## 06.09. Human Evaluation for HRI AI Models

![](images/image9.png){width="7.268055555555556in" height="7.268055555555556in"}

인간-로봇 상호작용 인공지능 모델(Human-Robot Interaction AI Model)을 위한 인간 평가(Human Evaluation)는 로봇의 행동이 시스템과 상호작용하는 사람의 관점에서 이해 가능하고, 적절하며, 신뢰할 수 있고, 편안하며, 효과적인지를 판단한다. 자동화 지표(Automated Metric)는 탐지 정확도, 작업 성공률, 지연시간 또는 충돌률을 정량화할 수 있지만 로봇의 의도에 대한 인간의 해석을 완전히 표현할 수는 없다. 따라서 인간-로봇 상호작용(HRI) 평가는 객관적인 행동 측정(Objective Behavioral Measurement)과 구조화된 관찰(Structured Observation), 주관적 판단(Subjective Judgment)을 결합해야 한다.

인간 평가(Human Evaluation)는 명확하게 정의된 상호작용 목표(Interaction Objective)와 사용자 역할(User Role)에서 시작해야 한다. 참가자는 로봇과 협업하거나, 지원을 받거나, 명령을 내리거나, 물리적 공간을 공유하거나, 자율 행동을 관찰할 수 있다. 평가 프로토콜(Evaluation Protocol)은 해당 맥락에서 성공적인 상호작용이 무엇을 의미하는지 명확하게 정의해야 한다. 평가 지표는 실제 작업과 연관되지 않은 일반적인 만족도 질문을 적용하기보다 인간과 로봇 사이에서 의도된 관계에 대응해야 한다.

작업 효과성(Task Effectiveness)은 인간-로봇 상호작용 평가의 중요한 기반을 제공한다. 연구자는 참가자가 협업 작업을 성공적으로 완료하는지, 완료에 얼마나 많은 시간이 필요한지, 얼마나 자주 지원이 필요한지, 그리고 얼마나 많은 상호작용 오류(Interaction Error)가 발생하는지를 측정할 수 있다. 이러한 객관적인 결과는 단순히 사회적으로 적절해 보이는 로봇과 실제로 인간의 목표 달성을 지원하는 로봇을 구분하는 데 도움이 된다. 따라서 인간의 평가는 관찰 가능한 작업 결과와 함께 해석해야 한다.

인지된 안전성(Perceived Safety)은 사용자가 로봇과 상호작용하면서 물리적으로 안전하다고 느끼는지를 측정한다. 이러한 인식은 공학적 안전성(Engineering Safety)과 다를 수 있다. 기술적으로 안전한 궤적이라도 사람에게는 갑작스럽거나, 지나치게 가깝거나, 예측하기 어려운 움직임으로 보일 수 있기 때문이다. 평가에서는 로봇 속도, 접근 방향, 이격 거리(Separation Distance), 로봇 팔 움직임, 정지 동작, 복구 행동에 대한 편안함을 조사할 수 있다. 인지된 안전성은 정량적인 물리적 안전 검증(Physical Safety Validation)을 대체하는 것이 아니라 이를 보완해야 한다.

신뢰(Trust)는 사람이 자율적인 로봇 행동에 언제 의존할 것인지를 결정해야 하므로 인간-로봇 상호작용의 핵심 특성이다. 지나친 불신은 불필요한 감독을 증가시키고 생산성을 저하시킬 수 있으며, 지나친 신뢰는 불완전한 시스템에 부적절하게 의존하도록 만들 수 있다. 따라서 인간 평가에서는 단순히 보고된 신뢰 수준을 최대화하는 것이 아니라 보정된 신뢰(Calibrated Trust)를 평가해야 한다. 즉 참가자의 신뢰가 실제로 확인된 로봇 능력, 불확실성, 실패, 복구 성능에 따라 적절하게 변화하는지를 확인해야 한다.

예측 가능성(Predictability)은 사용자가 로봇이 다음에 어떤 행동을 수행할 가능성이 있는지를 예상할 수 있는지를 의미한다. 로봇이 작업을 성공적으로 완료하더라도 주변 사람을 놀라게 하는 움직임이나 결정을 수행할 수 있다. 참가자는 내비게이션 경로, 조작 행동, 일시 정지, 시선 행동(Gaze Behavior), 언어 응답 등이 다음 행동을 예상하기 위한 충분한 단서를 제공하는지를 평가할 수 있다. 예측 가능한 상호작용은 인간과 로봇이 공유 작업공간(Shared Workspace)에서 움직임을 조정해야 할 때 특히 중요하다.

의도 명확성(Legibility)은 예측 가능성과 관련되어 있지만 로봇의 행동이 그 행동의 목표나 의도를 얼마나 명확하게 전달하는지에 초점을 둔다. 예를 들어 물체를 향해 손을 뻗는 궤적(Reaching Trajectory)은 물리적으로 효율적이면서도 로봇이 어떤 객체를 파지하려는 것인지 명확하지 않을 수 있다. 인간 평가에서는 관찰자가 로봇 행동의 일부만 보고도 목적지, 목표 객체, 의도된 전달 동작(Handover), 내비게이션 목표를 정확하게 추론할 수 있는지를 시험할 수 있다. 높은 의도 명확성은 불확실성을 줄이고 인간과 로봇 사이의 협응을 향상시킬 수 있다.

사용성 평가(Usability Evaluation)는 사람이 인간-로봇 상호작용 시스템을 얼마나 쉽게 조작하고, 명령하고, 감독하거나 협업할 수 있는지를 평가한다. 관련 관찰 항목에는 작업 학습시간(Task-Learning Time), 명령 오류, 반복 명령, 인터페이스 탐색의 어려움, 지원 요청 등이 포함될 수 있다. 주관적 평가에서는 사용 편의성(Ease of Use), 정신적 노력(Mental Effort), 만족도를 평가할 수 있다. 시스템의 한계에 익숙한 개발자는 인터페이스의 문제점을 무의식적으로 보완할 수 있으므로 실제 사용자를 대표하는 참가자를 포함하여 평가해야 한다.

인지 부하(Cognitive Workload)는 사람이 AI 기반 로봇을 지속적으로 감시하거나 협력해야 하는 경우 중요한 평가 요소이다. 작업을 성공적으로 완료하더라도 지속적인 인간의 주의를 요구하는 시스템은 실질적인 이점이 제한될 수 있다. 인지 부하는 구조화된 설문지(Structured Questionnaire), 보조 작업 성능(Secondary-Task Performance), 응답시간, 오류 패턴 또는 기타 검증된 방법을 통해 평가할 수 있다. 평가에서는 자동화가 실제로 인간의 부담을 감소시키는지, 아니면 물리적 작업의 부담을 감독과 해석의 부담으로 단순히 이전하는지를 판단해야 한다.

통신 품질(Communication Quality)은 음성, 텍스트, 제스처, 시선, 디스플레이, 조명 또는 다중모달 신호(Multimodal Signal)를 사용하는 로봇에서 평가해야 한다. 평가 지표는 명령이 올바르게 이해되는지, 로봇의 응답이 관련성이 있는지, 사용자가 불확실성이나 명확화 요청(Clarification Request)을 인식할 수 있는지를 조사할 수 있다. 언어 기반 AI 모델(Language-Enabled AI Model)에서는 의미론적 정확성(Semantic Correctness)만으로 충분하지 않으며, 통신은 적절한 시점에 이루어지고 현재의 물리적 상호작용 상태에 기반해야 한다.

명령 수행 평가(Instruction-Following Evaluation)는 하나의 명령에 여러 가지 합리적인 해석이 가능한 경우 인간의 판단을 포함해야 한다. 참가자는 로봇의 행동이 사전에 정의된 하나의 기준 행동(Reference Action)과 일치하는지만 판단하는 것이 아니라 명령의 명백한 의도와 일치하는지를 평가할 수 있다. 테스트에는 적절한 경우 바꿔쓰기(Paraphrase), 불완전한 지시 대상, 수정 명령(Correction), 후속 명령(Follow-Up Command)을 포함해야 한다. 이를 통해 AI 모델이 사용자가 기계 중심의 경직된 명령 패턴을 학습하도록 요구하지 않고 자연스러운 상호작용을 지원하는지를 평가할 수 있다.

오류 및 복구 행동(Error and Recovery Behavior)은 사용자의 인식에 큰 영향을 미친다. 로봇은 때때로 명령을 잘못 이해하거나, 객체 파지에 실패하거나, 경로가 차단되거나, 상호작용 상태를 추적하지 못할 수 있다. 인간 평가에서는 실패를 사용자가 인식할 수 있는지, 설명이 유용한지, 복구 행동(Recovery Action)이 적절하게 보이는지를 확인해야 한다. 참가자는 높은 확신을 보이면서 설명 없이 실패하는 로봇보다 불확실성을 투명하게 나타내고 예측 가능한 방식으로 복구하는 로봇을 선호할 수 있다.

경험에 따라 변화하는 특성을 평가하기 위해서는 반복 상호작용(Repeated Interaction)이 필요하다. 첫인상(First Impression)은 사용자가 로봇의 성공적인 행동과 실패 행동을 모두 경험한 이후에 형성되는 판단과 크게 다를 수 있다. 종단적 연구(Longitudinal Study) 또는 반복 세션 연구(Repeated-Session Study)를 통해 신뢰가 적절하게 보정되는지, 사용자가 로봇의 한계를 학습하는지, 불편함이나 인지 부하가 시간에 따라 증가하는지를 확인할 수 있다. 따라서 짧은 시연만으로 장기적인 수용성(Long-Term Acceptance)을 충분히 입증했다고 판단해서는 안 된다.

참가자 선정(Participant Selection)은 의도된 실제 배치 사용자 집단(Deployment Population)을 반영해야 한다. 로봇 사용 경험, 기술적 배경, 연령 범위, 전문적 역할, 목표 작업에 대한 친숙도는 상호작용 행동과 평가 결과에 영향을 줄 수 있다. 평가 보고서는 개인정보를 보호하면서 결과 해석에 필요한 참가자 특성을 설명해야 한다. 특정 전문 작업환경을 대상으로 하는 로봇을 로보틱스 연구자만 대상으로 시험한다면 실제 운영자를 위한 사용성에 대한 근거는 제한적일 수 있다.

실험 설계(Experimental Design)는 편향(Bias)과 교란 요인(Confounding Factor)을 줄여야 한다. AI 모델이나 상호작용 전략을 비교하는 경우 가능한 범위에서 참가자에게 동일한 작업 조건을 제공해야 한다. 시스템에 대한 사전 지식이 평가 결과에 영향을 줄 수 있다면 모델의 정체를 숨길 수 있으며, 학습 효과나 피로 효과(Fatigue Effect)를 줄이기 위해 조건의 순서를 균형화(Counterbalancing)할 수 있다. 표준화된 지침(Standardized Instruction)과 일관된 실험 진행자의 행동은 주관적 비교의 재현성을 향상시킨다.

설문지(Questionnaire)는 서로 관련되지 않은 여러 인상을 하나의 일반적인 선호도 점수로 결합하기보다 명확하게 정의된 평가 구성개념(Construct)을 사용해야 한다. 신뢰, 인지된 안전성, 사용성, 인지 부하, 사회적 수용성(Social Acceptance), 예측 가능성, 편안함은 서로 다른 상호작용 차원을 나타낸다. 적절한 경우 검증된 설문지를 사용해야 하며, 사용자 정의 질문(Custom Question)을 사용하는 경우에는 정확한 내용을 문서화해야 한다. 평가 척도(Rating Scale), 기준점(Anchor), 설문 시행 시점, 점수 계산 절차는 비교 대상 조건에서 일관되게 유지해야 한다.

정성적 피드백(Qualitative Feedback)은 수치 점수만으로 설명하기 어려운 실패 모드(Failure Mode)를 발견할 수 있다. 인터뷰, 개방형 의견(Open-Ended Comment), 사고 구술 관찰(Think-Aloud Observation), 작업 후 토론(Post-Task Discussion)을 통해 혼란스러운 행동, 불편한 움직임, 부족한 피드백, 예상하지 못한 사용자 전략을 발견할 수 있다. 정성적 결과는 단순한 사례를 선택적으로 제시하는 것이 아니라 체계적으로 코딩(Coding)해야 한다. 이러한 결과는 가설을 생성하고 후속 정량 평가 프로토콜을 개선하는 데 특히 유용하다.

통계 분석(Statistical Analysis)은 인간 대상 데이터(Human-Subject Data)의 구조를 반영해야 한다. 개인 간 차이는 클 수 있으며 동일한 참가자에게서 반복적으로 수집된 관측값은 서로 독립적이지 않고, 주관적 평가 척도는 제한된 해상도를 가질 수 있다. 따라서 보고서에서는 평균값만 사용하는 것이 아니라 표본 크기(Sample Size), 변동성(Variability), 신뢰구간(Confidence Interval), 적절한 비교 방법을 포함해야 한다. 효과 크기(Effect Size)는 통계적으로 관찰된 차이가 실제 상호작용 품질 측면에서도 의미가 있는지를 판단하는 데 유용할 수 있다.

윤리 및 개인정보 보호 고려사항(Ethical and Privacy Considerations)은 인간-로봇 상호작용 평가의 필수적인 구성요소이다. 참가자는 적용되는 연구 절차에 따라 상호작용의 성격, 수집되는 데이터, 관련 실험 위험을 이해해야 한다. 오디오, 비디오, 생리적 신호(Physiological Signal), 음성, 행동 로그(Behavioral Log)에는 민감한 정보가 포함될 수 있으므로 평가의 개인정보 보호 요구사항에 따라 처리해야 한다. 또한 예상하지 못한 로봇 행동이나 시스템 고장이 발생하는 경우에도 참가자를 보호할 수 있도록 안전 절차(Safety Procedure)를 마련해야 한다.

완전한 인간 평가 기록(Human-Evaluation Record)에는 AI 모델 버전, 로봇 구성, 작업 시나리오, 상호작용 인터페이스, 참가자 기준, 실험 절차, 설문지, 행동 지표, 분석 방법을 보존해야 한다. 필요한 경우 로봇 행동, 작업 결과, 개입(Intervention), 실패, 타이밍 정보를 인간의 평가 결과와 시간적으로 동기화해야 한다. 이를 통해 주관적 경험의 변화를 단순히 독립된 의견으로 취급하지 않고 특정 시스템 행동과 연결하여 분석할 수 있다.

궁극적으로 인간-로봇 상호작용 AI 모델을 위한 인간 평가(Human Evaluation for HRI AI Models)는 기술적으로 우수한 로봇 지능이 사람과의 효과적이고 수용 가능한 상호작용으로 실제 전환되는지를 판단해야 한다. 작업 성능(Task Performance)은 기능적 가치를 나타내며, 인지된 안전성, 보정된 신뢰, 예측 가능성, 의도 명확성, 사용성, 인지 부하, 통신 품질은 인간의 상호작용 경험을 특성화한다. 통제된 실험, 행동 기반 증거(Behavioral Evidence), 주관적 측정, 정성적 피드백을 결합하면 실제 배치 전에 인간-로봇 상호작용 시스템을 검증하기 위한 실용적인 기반을 구축할 수 있다.

## 06.10. AI Model Evaluation Dashboard and Reporting [w/Code]

![](images/image10.png){width="7.268055555555556in" height="7.268055555555556in"}

AI 모델 평가 대시보드(AI Model Evaluation Dashboard)는 로봇 AI 모델이 통합(Integration), 검증(Validation), 배치(Deployment)에 준비되었는지를 판단하는 데 필요한 평가 근거를 통합된 형태로 제공한다. 정확도, 작업 성공률, 지연시간, 안전성, 강건성을 서로 분리된 결과로 제시하는 대신 대시보드는 모델 버전과 운영 요구사항을 중심으로 이를 체계적으로 구성한다. 효과적인 보고(Reporting)는 복잡한 모델 동작을 하나의 종합 점수로 단순화하지 않으면서 엔지니어가 성능 향상, 회귀(Regression), 상충관계(Tradeoff), 해결되지 않은 위험을 식별할 수 있도록 해야 한다.

대시보드는 명확하게 정의된 평가 범위(Evaluation Scope)에서 시작해야 한다. 각 보고서에는 모델, 로봇 플랫폼, 작업 영역(Task Domain), 데이터셋 또는 시나리오 집합, 하드웨어 구성, 소프트웨어 버전, 평가 날짜를 명시해야 한다. 또한 의도된 운영 조건과 허용 기준(Acceptance Criteria)을 확인할 수 있어야 한다. 이러한 맥락 정보는 서로 다른 가정 아래 생성된 지표를 동일한 실험 결과처럼 비교하는 것을 방지하고 시스템이 변화한 이후에도 과거 결과를 올바르게 해석할 수 있도록 한다.

모델 식별(Model Identification)과 추적성(Traceability)은 기본적인 요구사항이다. 모든 결과는 변경 불가능한 모델 버전, 체크포인트(Checkpoint), 구성, 추론 엔진(Inference Engine), 수치 정밀도(Numerical Precision), 관련 전처리 파이프라인(Preprocessing Pipeline)과 연결되어야 한다. 필요한 경우 학습 데이터 또는 평가 데이터 버전도 기록해야 한다. 추적성을 확보하면 결과를 재현하고 특정 변경 사항과 성능 회귀를 연계할 수 있으며, 벤치마크 수치가 해당 결과를 생성한 정확한 모델 산출물(Model Artifact)과 분리되는 것을 방지할 수 있다.

대시보드의 주요 계층(Primary Dashboard Layer)은 모델 기능에 대응하는 핵심 성능 지표(Key Performance Indicator, KPI)를 요약해야 한다. 인식 모델(Perception Model)은 평균 정밀도(mAP), 교차영역비(IoU), 궤적 오차(Trajectory Error), 추적 품질(Tracking Quality)을 보고할 수 있으며, 내비게이션 정책(Navigation Policy)은 성공률(Success Rate), 경로 길이 가중 성공률(SPL), 내비게이션 오차(Navigation Error)를 보고할 수 있다. 조작, 이동, 비전-언어-행동(VLA), 인간-로봇 상호작용(HRI) 등의 모델에도 각각 작업에 적합한 지표가 필요하다. 공통 대시보드는 서로 다른 AI 능력을 인위적인 하나의 범용 지표로 통합하기보다 이러한 차이를 유지해야 한다.

작업 성공(Task Success)은 성공의 의미를 설명할 수 있는 충분한 맥락과 함께 제시해야 한다. 작업 정의, 허용 오차(Tolerance), 종료 조건(Termination Condition), 시험 횟수를 알 수 없다면 성공률 하나만으로는 의미가 불명확하다. 따라서 대시보드는 성공 지표를 시나리오 수와 평가 조건에 연결해야 한다. 여러 단계로 구성된 작업에서는 하위 작업 완료(Subtask Completion)를 함께 표시하여 전체 점수가 안정적으로 보이더라도 인식, 계획, 파지, 복구 또는 작업 종료 과정에서 반복적인 실패가 발생하는지를 확인할 수 있도록 해야 한다.

분포 기반 보고(Distributional Reporting)는 평균값만 표시하는 것보다 더 많은 정보를 제공한다. 평가 대시보드는 필요한 경우 중앙값, 백분위수(Percentile), 변동성(Variability), 신뢰구간(Confidence Interval), 최악 조건 동작(Worst-Case Behavior)을 보여주어야 한다. 평균 성능은 우수하지만 심각한 꼬리 영역 실패(Tail Failure)가 발생하는 모델은 물리적 시스템의 실제 배치에 부적합할 수 있다. 또한 모델 릴리스별 결과 분포의 이력을 비교하면 성능 향상이 전반적인 개선인지 아니면 제한된 일부 평가 사례에서만 나타난 것인지를 판단할 수 있다.

시나리오 수준 분석(Scenario-Level Breakdown)은 모델의 강점과 약점을 명확하게 보여주어야 한다. 결과는 객체 유형, 환경, 지형, 조명, 작업 난이도, 사용자 조건, 분포 변화 범주(Distribution-Shift Category) 또는 기타 운영 변수에 따라 구분할 수 있다. 이러한 세분화(Slicing)는 쉬운 평가 사례가 전체 지표를 지배하는 것을 방지한다. 또한 엔지니어링 팀이 특정 운영 조건과 성능 회귀를 연결하여 추가 학습, 센서 변경, 폴백 동작(Fallback Behavior), 배치 제한(Deployment Restriction)이 필요한지를 결정할 수 있도록 한다.

분포 외 강건성(Out-of-Distribution Robustness)은 종합적인 분포 내 성능만으로 실제 배치 신뢰성을 입증할 수 없으므로 전용 보고 화면을 가져야 한다. 대시보드는 분포 변화 범주와 심각도 수준(Severity Level)에 따라 기준 성능과 분포 외(OOD) 결과를 비교하고 상대적인 성능 저하를 표시할 수 있다. 가능한 경우 불확실성 동작(Uncertainty Behavior), OOD 탐지, 복구 성능, 폴백 활성화(Fallback Activation)도 보고해야 한다. 이러한 화면은 추가적인 안전장치 없이 모델 동작을 신뢰해서는 안 되는 운영 경계를 정의하는 데 도움이 된다.

안전 관련 결과(Safety-Related Result)는 일반적인 성능 지표와 명확하게 구분되어야 한다. 충돌 이벤트, 위험한 접촉, 전도 이벤트(Fall Event), 안전 제어기 개입(Safety-Controller Intervention), 제약 조건 위반, 비상 정지(Emergency Stop), 기타 모델별 위험 요소는 종합 점수 내부에 숨겨져서는 안 된다. 작업 성공률이 향상되었더라도 심각한 안전 이벤트가 증가했다면 실제 배치 관점에서는 성능 회귀로 판단해야 한다. 따라서 안전 허용 기준(Safety Acceptance Criteria)은 명시적인 통과(Pass), 실패(Fail), 검토(Review) 상태를 지원해야 한다.

지연시간, 계산 부하(Computational Load), 에너지 결과는 이를 지원하는 모델 품질 지표(Model-Quality Metric)와 직접 연결되어야 한다. 대시보드는 중앙값 및 꼬리 추론 지연시간(Tail Inference Latency), 처리량(Throughput), 데드라인 위반(Deadline Violation), 메모리 사용량, 프로세서 활용률, 평균 및 최대 전력, 추론당 에너지(Energy per Inference)를 보고할 수 있다. 이러한 결과는 정확한 실제 배치 하드웨어와 런타임 구성(Runtime Configuration)을 참조해야 한다. 효율성과 품질을 연결하면 양자화(Quantization), 모델 압축(Model Compression), 해상도 감소 또는 추론 주파수 감소에 따른 상충관계를 명확하게 확인할 수 있다.

인간-로봇 상호작용 모델(HRI Model)의 경우 객관적인 작업 결과와 구조화된 인간 평가(Human Evaluation)를 결합하여 보고해야 한다. 작업 완료, 상호작용 오류, 개입 빈도(Intervention Frequency), 응답시간을 인지된 안전성(Perceived Safety), 신뢰(Trust), 사용성(Usability), 인지 부하(Workload), 예측 가능성(Predictability), 통신 품질(Communication Quality) 등의 평가 결과와 함께 제시할 수 있다. 필요한 경우 인간 평가에는 참가자 수와 불확실성 정보도 포함해야 한다. 중요한 사용성 문제가 수치 평균에 가려지지 않도록 정성적 결과(Qualitative Finding)는 별도로 요약할 수 있다.

지속적인 모델 개발(Continuous Model Development)을 위해서는 추세 보고(Trend Reporting)가 필수적이다. 대시보드는 모델 버전, 소프트웨어 릴리스, 데이터셋, 하드웨어 구성 사이에서 비교 가능한 지표를 표시하는 동시에 평가 조건이 변경된 경우 잘못된 비교를 방지해야 한다. 회귀 임계값(Regression Threshold)을 사용하면 통계적 또는 운영적으로 의미 있는 성능 저하를 식별할 수 있다. 과거 기준선(Historical Baseline)과 릴리스 후보(Release Candidate)를 유지하면 한 가지 능력의 개선이 다른 능력의 희생을 통해 달성된 것인지 판단할 수 있다.

자동화된 회귀 보고(Automated Regression Reporting)는 모델 평가를 지속적 통합(Continuous Integration) 및 검증 워크플로(Validation Workflow)와 연결할 수 있다. 새로운 모델 산출물이 생성되면 표준화된 평가 스위트(Standardized Evaluation Suite)가 지표를 생성하고 승인된 기준선과 비교할 수 있다. 보고서는 임계값 초과, 누락된 테스트, 새로운 실패, 중요한 분포 변화를 표시할 수 있다. 자동화는 수동 해석 오류를 줄일 수 있지만 최종 배치 결정은 자동화된 게이트(Automated Gate)에만 의존하지 않고 시나리오의 맥락과 안전 중요성을 함께 고려해야 한다.

실패 보고(Failure Reporting)는 요약 지표와 실제로 조사할 수 있는 평가 근거를 연결해야 한다. 엔지니어는 성능이 저하된 점수에서 해당 시나리오, 센서 관측, 모델 출력, 로봇 궤적, 작업 상태, 타이밍 정보, 종료 원인(Termination Cause)까지 추적할 수 있어야 한다. 실패 범주는 인식 오류, 잘못된 행동, 위치 추정 손실(Localization Loss), 불안정한 제어, 시간 초과(Timeout), 안전 시스템 개입, 복구 실패 등을 포함할 수 있다. 이러한 연결을 통해 대시보드는 단순한 점수 표시 화면이 아니라 엔지니어링 진단 시스템(Engineering Diagnostic System)으로 기능할 수 있다.

비교 보고(Comparative Reporting)는 모델 선택 과정을 투명하게 만들어야 한다. 후보 모델은 동일한 시나리오와 하드웨어를 사용하여 공통 기준선(Common Baseline)과 비교할 수 있으며, 작업 품질, 강건성, 지연시간, 에너지, 메모리, 안전성의 차이를 함께 보여줄 수 있다. 비교에서는 하나의 지표만으로 최적 모델을 선언하기보다 상충관계를 강조해야 한다. 정확도가 약간 낮은 모델이라도 지연시간이 훨씬 짧고, OOD 동작이 강건하며, 에너지 소비량이 낮거나, 실패 특성(Failure Characteristic)이 더 예측 가능하다면 실제 배치에서는 더 적합할 수 있다.

허용 기준(Acceptance Criteria)은 결과를 관찰한 이후 임의로 선택하는 것이 아니라 시스템 및 배치 요구사항에서 도출해야 한다. 중요한 각 지표에는 필요한 경우 목표값(Target), 경고 범위(Warning Range), 허용 불가 영역(Unacceptable Region)을 정의할 수 있다. 일부 기준은 시스템 전체에 공통으로 적용될 수 있지만 다른 기준은 시나리오 심각도나 안전 등급(Safety Classification)에 따라 달라질 수 있다. 명확한 임계값을 사용하면 릴리스 결정을 일관되게 수행할 수 있으며 모델이 배치 준비 완료, 조건부 허용 또는 추가 검증 필요 상태인지를 대시보드에서 명확하게 전달할 수 있다.

보고 시스템은 데이터 커버리지(Data Coverage)와 평가 완전성(Evaluation Completeness)도 전달해야 한다. 의도된 운영 영역의 제한된 일부만 시험했다면 높은 점수의 의미는 제한적이다. 대시보드는 평가에 포함된 시나리오 수, 반복 시험 횟수, 환경 조건, 객체 범주, OOD 수준, 하드웨어 구성, 해결되지 않은 테스트 공백(Test Gap)을 보여줄 수 있다. 커버리지 정보는 충분한 평가 근거에 기반한 높은 성능과 불충분한 시험에서 얻어진 높은 성능을 구분하는 데 도움이 된다.

재현성(Reproducibility)을 확보하려면 대시보드가 평가 결과와 함께 평가 메타데이터(Evaluation Metadata)를 보존해야 한다. 모델 식별자, 데이터셋 버전, 시나리오 정의, 난수 시드(Random Seed), 센서 구성, 하드웨어, 추론 설정, 소프트웨어 의존성(Software Dependency), 평가 스크립트, 지표 정의를 기록해야 한다. 가능한 경우 원시 로그(Raw Log)와 파생 보고서(Derived Report)를 서로 연결하여 유지해야 한다. 이를 통해 이후 감사(Audit) 과정에서 보고된 값이 어떻게 생성되었는지를 재구성하고 평가 파이프라인이 변경되더라도 신뢰할 수 있는 비교를 수행할 수 있다.

서로 다른 사용자 집단은 서로 다른 수준의 보고 상세도(Reporting Depth)를 필요로 한다. 연구자는 상세한 분포와 실패 사례를 필요로 할 수 있고, 로보틱스 엔지니어는 시스템 통합 및 실행시간 제약에 집중할 수 있으며, 안전 담당자는 위험 관련 평가 근거를 요구할 수 있다. 관리자는 릴리스 상태와 주요 위험에 관심을 가질 수 있다. 계층형 대시보드(Layered Dashboard)는 서로 충돌하는 별도의 보고서를 유지하지 않고도 이러한 사용자 집단을 지원할 수 있다. 요약 화면의 결론은 항상 해당 결론의 기반이 된 상세 기술 근거까지 추적할 수 있어야 한다.

궁극적으로 AI 모델 평가 대시보드(AI Model Evaluation Dashboard)는 단순히 보기 좋은 차트의 집합이 아니라 로봇 AI 개발을 위한 평가 근거 관리 계층(Evidence-Management Layer)으로 기능해야 한다. 모델 식별, 작업 성능, 강건성, 안전성, 인간 평가, 지연시간, 에너지, 커버리지, 실패 근거를 재현 가능한 보고 구조 안에서 연결해야 한다. 이러한 대시보드를 회귀 테스트(Regression Testing) 및 릴리스 기준(Release Criteria)과 통합하면 방어 가능한 모델 선택, 엔지니어링 진단, 검증, 실제 배치 결정을 지원할 수 있다.
