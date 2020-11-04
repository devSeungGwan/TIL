# Neural Compute Stick

## 목적

메리 과제를 수행할 때 필요한 종단지능단말(AI Edge)에 대한 시험이 필요한 Neural Compute Stick에 대한 테스트 시나리오를 설명한다. 

AI Edge 기능을 담당할 H/W 중 가장 최적화 된 제품을 실험하기 위해 해당 제품을 사용한다. 또한 정반 내 카메라가 여러군데 위치하기 때문에 하나의 Main Server 에서 모든 연산을 처리하는 것보다, Edge에서 분산처리하여 시스템을 운영하는 것이 적합하다. 

메리 과제에 비용 대비 효익 (Benefit to Cost) 차원에서 가장 적합한 AI Edge솔루션을 구축하기 위한 “원점 (Ground-zero reference)”자료로써, 본 문서를 작성한다.

## 개요

Intel® Neural Compute Stick 2는 Intel™ Movidius™ VPU를 기반으로 업계 최고의 성능, 와트 및 성능을 제공합니다. NEURAL COMPUTE는 솔루션 개발 속도를 가속화하고 배치를 원활하게 하는 툴키트인 OpenVINO™를 지원합니다. Neural Compute Stick 2는 플러그 앤 플레이를 간소화하고 일반적인 프레임워크 및 즉시 사용 가능한 샘플 애플리케이션을 지원합니다. USB 포트가 있는 플랫폼을 사용하면 클라우드 컴퓨팅에 의존하지 않고 프로토타입을 제작하고 운영할 수 있습니다. Intel NCS 2는 이전 세대에 비해 성능이 8배 향상되어 초당 4조회의 연산 작업을 수행합니다.

## 특징

- **생산성 향상**

  - 프로토타입 제작 시간 단축 또는 저렴한 비용으로 다목적 하드웨어 처리 성능을 제공하도록 신경망 네트워크 튜닝

  - 향상된 하드웨어 처리 성능과 본래의 Intel Movidius Neural Compute Stick 비교

  - 12개 대신 16개 코어를 활용하고 신경 컴퓨팅 엔진, 전용 딥 신경 네트워크 가속기 사용

  - 네트워크에 따라 딥 신경망 추론 시 최대 8 배의 성능 향상

  - 적절한 가격으로 신경 네트워크 애플리케이션 가속화

  - AI 개발 키트 환경 변화

  - 플러그 앤 플레이 간소화

  - 저렴한 가격대

  - 공통 프레임워크 지원 및 즉시 사용 가능하고 신속한 개발 구현

    

- **효율성 발견**

  - 머신 비전을 개선하는 와트 당 탁월한 성능

  - 클라우드 컴퓨팅 연결에 의존하지 않고 "가장자리에서" 실행

  - 랩톱, 단일 보드 컴퓨터 또는 USB 포트가 있는 모든 플랫폼에 심층 학습 프로토타이핑 제공 가능

  - 접근성이 뛰어나고 경제적임 - 와트 당 더 우수한 성능과 효율적인 팬리스 설계 활용

  - Intel® Movidius™ Myriad™ X VPU의 하드웨어 최적화 성능과 Intel® Distribution of OpenVINO 툴키트를 결합하여 딥 신경 네트워크 기반 애플리케이션 가속화

  - 동급 최강인 Neural Compute Engine - 전용 하드웨어 가속기

  - SHAVE 코어라 불리는 16개의 강력한 프로세싱 코어와 초고속 처리량 지능형 메모리 패브릭 특징 덕분에 Intel Movidius Myriad X VPU가 온 디바이스 딥 신경 네트워크 및 컴퓨터 비전 애플리케이션의 업계 최고의 제품이 됨

  - 칩에 완전히 새로운 딥 신경 네트워크(DNN) 추론 엔진 탑재

    

- **프로토타이핑을 위한 보다 단순한 다기능**

  - Intel® Distribution of OpenVINO 툴키트가 개발 환경을 원활하게 만듬
  - Intel Neural Compute Stick 2의 프로토타입을 제작한 다음 딥 신경 네트워크를 Intel Movidius Myriad X VPU 기반 임베디드 장치에 배포
  - 작동 프로토타입 측 경로 능률화
  - Intel 하드웨어에서 워크로드 확장 및 성능 극대화
  - 견고한 Intel Distribution of OpenVINO 키트를 통해 인간의 시각을 에뮬레이트하는 애플리케이션과 솔루션을 보다 쉽게 연결하고 배포 가능
  - Intel Distribution of OpenVINO 툴키트는 다중 플랫폼 컴퓨터 비전 솔루션의 개발을 원할하게 하고 심층 학습 성능을 증대함
  - 이제 애플리케이션 개발이 훨씬 쉬워져 일련의 Intel 가속 기술을 통해 이기 방식으로 기능을 실행할 수 있습니다. 한 번 개발하고 Intel CPU, VPU, 통합 그래픽 또는 FPGA에 배포할 수 있습니다.
  - 원할 경우 사용자는 자신의 맞춤 레이어를 구현하고 나머지 모델이 VPU에서 실행되는 동안 CPU에서 실행 가능

![Block Diagram - Intel Neural Compute Stick 2](https://kr.mouser.com/images/marketingid/2018/microsites/153249968/NeuralComputeStick2BD.png)

> 그림 1. Neural Compute Stick Architecture 

## 형상

![img](http://vctec.co.kr/web/product/sparkfun/img/15343-1.jpg)

> 그림 2. Neural Compute Stick 2 형상

## 제원

- Processor: Intel® Movidius™ Myriad™ X Vision Processing Unit (**VPU**)
- Supported frameworks: **TensorFlow* and Caffe***
- Connectivity: USB 3.0 Type-A
- Dimensions: 2.85 in. x 1.06 in. x 0.55 in. (72.5 mm x 27 mm x 14 mm)
- Operating temperature: 0° C to 40° C
- Compatible operating systems: **Ubuntu* 16.04.3 LTS (64 bit), CentOS* 7.4 (64 bit), and Windows® 10 (64 bit)**

