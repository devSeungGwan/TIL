구글, 마이크로소프트, 아마존 등 IT 기업들이 클라우드 컴퓨팅 인프라를 제공하고 있고, 클라우드 컴퓨팅을 통해 솔루션을 제공하고 있는 기업들이 늘어나고 있다. 정보 기술 연구 및 자문 회사인 가트너에서는 2017년부터 2021년까지 클라우드 컴퓨팅으로 벌어드리는 총 수익이 연간 30%씩 상승할 것이라 전망하였다. 이처럼 클라우드 컴퓨팅 시장이 커짐에 따라 IoT, AR 등 생활의 다양한 분야가 클라우드 컴퓨팅과 밀접한 관계를 가질 것이다.

클라우드 서비스 시장에서 가장 큰 점유율을 가진 기업은 아마존이다. 사용하지 않는 컴퓨팅 자원을 사용하여 클라우드 서비스인 AWS(Amazon Web Service)를 제공하고 있다. 현재 AWS의 시장 점유율은 33%이고 Microsoft Azure(16%), Google Cloud Platform(8%)로 구성되어 있다. 점유율 확보를 위해 클라우드 서비스 제공 기업들은 더 많은 리전을 설치하고 있고, 세분화 된 서비스를 구성하여 솔루션을 제공하고 있다.

클라우드 컴퓨팅은 다음과 같은 장점을 가진다.

- 인프라 구성을 쉽게 할 수 있다.
  - 데이터베이스, 서버를 구성하고 이들을 연결하기 위해 Message-Queue 서비스를 가져와서 연결하는 등 클라우드 내 구성되있는 리소스를 가져와서 서비스 구성을 할 수 있다.
  - 개발 속도 및 비용을 절감할 수 있다.
- 사용량(트래픽)에 따라 리소스의 크기를 변경할 수 있다.
  - 출퇴근 시간 같이 어플리케이션 사용량이 많을 때, 리소스 크기를 늘림으로 서비스를 유연하게 관리할 수 있다.
  - 서버를 여러 대 늘림으로 분산 처리에 유리하다.
  - 유지 비용 및 서비스의 안정성을 가져올 수 있다.
- 서비스의 배포가 용이하다.
  - 필요에 따라 서비스를 복사하여 다른 리전에 움겨 서비스가 가능하다.
  - 글로벌 서비스를 운용할 때 유용하다.

클라우드 컴퓨팅의 종류는 크게 세가지로 분류할 수 있다.

- 네트워크, 저장소, 컴퓨팅 엔진 등 리소스를 제공하는 **IaaS(Infastructure as a Service)**
- AutoML을 통해 머신러닝 모델과 파라미터를 찾아주거나 사용자가 관리하지 않아도 스스로 서비스를 동작시켜주는 Google App Engine 같은 **PasS(Platform as a Service)**
- 어플리케이션 수준에서 사용자에게 서비스를 제공하는 **SaaS(Software as a Service)**

------

# GCP 란

구글 검색과 유튜브와 같은 최종 사용자 제품을 위해 내부적으로 구글이 사용하는, 동일한 지원 인프라스트럭처 위에서 호스팅을 제공하는 구글의 클라우드 컴퓨팅 서비스이다.

GCP 데이터 센터를 설립한 리전은 총 20곳이 존재하며 대한민국(서울)에도 확장할 예정이다.

![https://cloud.google.com/images/locations/regions-2x.png?hl=ko](https://cloud.google.com/images/locations/regions-2x.png?hl=ko)

그림 2. 데이터 센터(리전) 위치

처음 사용자가 계정 생성 시 12개월동안 사용할 수 있는 $300 달러 크래딧을 제공한다. 처음 사용하는 개발자들을 위해 무료로 여러가지 기능들을 사용해보고, 개발해볼 수 있는 환경을 제공해준다.

또한 프리티어 제품군은 사용 범위 내에서 리소스를 사용했을 경우에는 크래딧을 따로 소모하지 않아도 무료로 사용이 가능하다. 이를 통해서 VM 이미지를 프리티어에서 제작 후 인프라 리소스 크기를 늘려 불필요한 지출없이 사용할 수 있다.

------

# GCP 리소스

리소스는 사용자가 GCP에서 사용할 수 있는 서비스들(데이터 센터에 위치한 컴퓨터, 하드 디스크 드라이브와 같은 물리 리소스, 가상 머신(VM)과 같은 가상 리소스)이다.

리소스의 범위에 따라 리전에 따른 엑세스 가능 여부가 달라진다. 한 리전에서 다른 리전으로 리소스를 연결한다고 하면 네트워크 지연 등으로 인해 성능이 감소할 수 있다. 그러므로 작업의 범위에 따라서 엑세스 할 수 있는 리소스의 범위를 파악하고 사용해야 한다.

리소스를 생성할 때는 프로젝트 내에 생성해야 한다. 프로젝트는 리소스를 관리 할 수 있도록 데이터 센터 내 사용자가 생성하고 프로젝트 내에 필요한 리소스를 추가하여 서비스를 구성할 수 있다.

**전역 리소스**

- 모든 리전에서 엑세스 가능
- 사전 구성된 디스크 이미지, 디스크 스냅샷, 네트워크

**지역 리소스**

- 일부 리소스는 같은 리전에 있는 리소스에서만 액세스 가능
- 고정 외부 IP 주소

**영역 리소스**

- 같은 영역에 있는 리소스에서만 액세스 가능
- VM 인스턴스, 인스턴스의 유형, 디스크

![https://cloud.google.com/docs/images/overview/regions-zones.svg?hl=ko](https://cloud.google.com/docs/images/overview/regions-zones.svg?hl=ko)

그림 3. 리소스 관계도

------

# GCloud

Google Cloud SDK를 로컬에 설치하여 GCP 리소스나 프로젝트를 관리할 때 사용하는 CLl(Command Line Interface)이다.

GCloud CLI를 사용하여 다음과 같은 작업을 실행할 수 있다.

- Google Compute Engine 가상 머신 인스턴스 및 기타 리소스
- Google Cloud SQL 인스턴스
- Google Kubernetes Engine 클러스터
- Google Cloud Dataproc 클러스터 및 작업
- Google Cloud DNS 관리 영역 및 레코드 조합
- Google Cloud Deployment Manager 배포

## GCloud 설치

mac 환경을 기준으로 설치를 진행한다.

원하는 위치에 wget 명령어를 사용하여 GCloud 설치 파일을 다운로드 받는다.

```bash
wget <https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-245.0.0-darwin-x86_64.tar.gz?hl=ko>
```

GCloud의 압축을 해제하고 자신의 Shell(bash, zsh 등)에 맞게 환경변수를 입력한다.

```bash
# 환경변수를 입력하기 위해 vi로 파일을 연다.
vi ~/.zshrc

# GCloud 환경 변수를 입력한다.
export GOOGLE_CLOUD_SDK_PATH=[google-cloud-sdk PATH]
export PATH=$PATH:$GOOGLE_CLOUD_SDK_PATH/bin

# 변경사항을 적용한다.
source ~/.zshrc
```

> zsh를 기준으로 작성하였다.

GCloud가 작동하는 지 확인한다.

```bash
gcloud --version
```

## Cloud Shell

GCP 리소스 및 서비스를 조정할 수 있는 웹 기반 쉘 환경이다.

Cloud Shell이 제공하는 기능은 다음과 같다.

- 임시 Compute Engine 가상 머신 인스턴스
- 웹 브라우저에서 인스턴스에 명령줄로 액세스
- 기본 제공 코드 편집기
- 5GB의 영구 디스크 저장소
- 사전 설치된 Google Cloud SDK 및 기타 도구
- 자바, Go, Python, Node.js, PHP, Ruby, .NET과 같은 언어 지원
- 웹 미리보기 기능
- GCP 콘솔 프로젝트 및 리소스 액세스를 위한 자체 승인 기능

------

# GCP 서비스 종류

GCP에서는 컴퓨팅, 네트워킹, 저장소, 빅데이터, 머신러닝 등 100가지가 넘는 다양한 종류의 서비스가 제공되고, 그 중에서 컴퓨팅 서버에 대해 자세하게 설명한다.

관리(Ops)의 비중에 따라 컴퓨팅 서버의 유형을 나눴다. 개발자의 서버 관리 비중이 높다면 IaaS의 측면에서 관리 사항은 많아지지만 유연하게 관리할 수 있다. 반면에 GCP의 관리 비중이 높아지면 PaaS의 측면에서 관리에 대한 비용을 적게 사용하지만, 사용자가 사용할 수 있는 기능에 제약이 생긴다.

![https://cloud.google.com/docs/images/overview/ops-continuum.svg](https://cloud.google.com/docs/images/overview/ops-continuum.svg)

그림 4. 관리 측면에서 본 컴퓨팅 서버 종류

## Cloud Function

- 클라우드 서비스를 연결하기 위한 서버리스(Serverless) 실행환경이다.
- 클라우드 인프라와 서비스에서 발생하는 이벤트에 연결되는 단일 목적의 간단한 함수를 작성할 수 있고, 특정 이벤트 발생 시 실행이 된다.
- 코드는 완전 관리형 환경에서 실행되므로, 인프라를 프로비저닝하거나 서버를 관리할 필요가 없다.
- Node.js(Node.js 6, 8 또는 10), Python 3(Python 3.7) 또는 Go(Go 1.11) 환경에서 실행할 수 있으므로, 이동성 및 로컬 테스트가 편리하다.

### 사용사례

**데이터 처리/ETL**

- 파일 생성, 변경 또는 삭제 시와 같이 Cloud Storage 이벤트를 리슨 및 응답한다.
- Cloud Functions에서 이미지 처리, 동영상 트랜스코딩 수행, 데이터 유효성 검사 및 변환, 인터넷 서비스 호출이 가능하다.

**웹훅**

- 간단한 HTTP 트리거를 통해 GitHub, Slack, Stripe와 같은 타사 시스템 또는 HTTP 요청을 보낼 수 있는 모든 곳에서 발생한 이벤트에 응답한다.

**경량형 API**

- 신속하게 빌드하고 즉시 확장되는 느슨하게 연결된 경량의 로직 비트로 애플리케이션을 작성한다.
- 함수는 이벤트 기반으로 작동하거나 HTTP/S를 통해 직접 호출한다.

**모바일 백엔드**

- Google의 앱 개발자용 모바일 플랫폼인 Firebase를 사용하여 Cloud Functions에서 모바일 백엔드를 작성한다.
- Firebase 애널리틱스, 실시간 데이터베이스, 인증, 스토리지에서 수신된 이벤트를 리슨 및 응답한다.

## App Engine

확장 가능한 웹 애플리케이션을 개발하고 호스팅하는 완전 관리형 서버리스 플랫폼(PaaS)이다. 사용자가 Javascript, Python 등으로 프로그램을 작성하고 App Engine에 앱을 등록하면 내부 런타임에 의해 자동으로 실행된다. 또한 리소스 관리도 자동으로 해준다. 트래픽이 몰려 리소스가 부족할 경우, App Engine에서 자동으로 리소스를 늘려 대처할 수 있도록 한다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c7665a1d-ab8a-4852-a8e4-97bbebb934a9/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c7665a1d-ab8a-4852-a8e4-97bbebb934a9/Untitled.png)

그림 5. APP Engine 개요

### 환경

App Engine은 표준환경과 가변형 환경으로 나뉠 수 있다.

표준 환경은 구글 앱 앤진 내부 샌드박스에 앱을 등록하여 실행하는 환경이다. App Engine이 자동으로 트래픽에 따라 오토 스케일링을 수행해준다. 이를 통해 안정된 앱 운영이 가능하다.

가변형 환경은 Compute Engine을 기반으로 작동한다. Compute Engine 위에서 앱을 실행하면 마이크로 서비스, 승인, SQL 및 NoSQL 데이터베이스, 트래픽 분할, 로깅, 버전 관리, 보안 스캔, 콘텐츠 전송 네트워크가 모두 기본적으로 지원한다.

아래는 표준 환경과 가변형 환경의 차이점에 따른 표를 나타냈다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0e288f59-a081-46c1-b495-5b426ae5b7c4/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0e288f59-a081-46c1-b495-5b426ae5b7c4/Untitled.png)

표 2. 표준 환경과 가변형 환경의 차이점(GCP 발췌)

## Kubernetes Engine

**서비스로써의 컨테이너(CaaS, Container as a Service)**

구글에서 제작한 Kubernetes 시스템을 기반으로 구축되었고, GCP의 공용 클라우드 인프라 뿐만 아니라, 온프레미스 또는 하이브리드 클라우드를 선택할 수 있는 유연성을 제공한다.

### **Kubernetes**

컨테이너화된 워크로드와 서비스를 관리하기 위한 이식성이 있고, 확장가능한 오픈소스 플랫폼이다.

구글이 15년에 거친 대규모 상용 워크로드 운영 경험을 바탕으로 2014년에 오픈소스로 공개했다.

기존 OS와 프로그램을 묶어서 배포하던 Virutal Machine과 다르게 기존에 있던 OS에 컨테이너 단위로 앱을 배포할 수 있다. VM에 비해 OS가 없으므로 상대적으로 가볍고, VM과 마찬가지로 다른 환경과 격리되어 실행된다.

![https://d33wubrfki0l68.cloudfront.net/26a177ede4d7b032362289c6fccd448fc4a91174/eb693/images/docs/container_evolution.svg](https://d33wubrfki0l68.cloudfront.net/26a177ede4d7b032362289c6fccd448fc4a91174/eb693/images/docs/container_evolution.svg)

그림 6. 배포 환경의 변화

Kubernetes는 다음과 같은 기능을 제공한다.

- 서비스 디스커버리와 로드 밸런싱
  - 쿠버네티스는 DNS 이름을 사용하거나 자체 IP 주소를 사용하여 컨테이너를 노출할 수 있다. 컨테이너에 대한 트래픽이 많으면, 쿠버네티스는 네트워크 트래픽을 로드밸런싱하고 배포하여 배포가 안정적으로 이루어질 수 있다.
- 스토리지 오케스트레이션
  - 쿠버네티스를 사용하면 로컬 저장소, 공용 클라우드 공급자 등과 같이 원하는 저장소 시스템을 자동으로 탑재 할 수 있다.
- 자동화된 롤아웃과 롤백
  - 쿠버네티스를 사용하여 배포된 컨테이너의 원하는 상태를 서술할 수 있으며 현재 상태를 원하는 상태로 설정한 속도에 따라 변경할 수 있다. 예를 들어 쿠버네티스를 자동화해서 배포용 새 컨테이너를 만들고, 기존 컨테이너를 제거하고, 모든 리소스를 새 컨테이너에 적용할 수 있다.
- 자동화된 빈 패킹(bin packing)
  - 컨테이너화된 작업을 실행하는데 사용할 수 있는 쿠버네티스 클러스터 노드를 제공한다. 각 컨테이너가 필요로 하는 CPU와 메모리(RAM)를 쿠버네티스에게 지시한다. 쿠버네티스는 컨테이너를 노드에 맞추어서 리소스를 가장 잘 사용할 수 있도록 해준다.
- 자동화된 복구(self-healing)
  - 쿠버네티스는 실패한 컨테이너를 다시 시작하고, 컨테이너를 교체하며, ‘사용자 정의 상태 검사’에 응답하지 않는 컨테이너를 죽이고, 서비스 준비가 끝날 때까지 그러한 과정을 클라이언트에 보여주지 않는다.
- 시크릿과 구성 관리
  - 쿠버네티스를 사용하면 암호, OAuth 토큰 및 ssh 키와 같은 중요한 정보를 저장하고 관리 할 수 있다. 컨테이너 이미지를 재구성하지 않고 스택 구성에 비밀을 노출하지 않고도 비밀 및 애플리케이션 구성을 배포 및 업데이트 할 수 있다.

## Compute Engine

**서비스로써의 인프라(IaaS, Infrastructure as a Service)**

컴퓨팅 인프라(CPU, GPU 등)은 제공하지만 OS나 런타임 등 플랫폼 구성 요소를 설계하고 모니터링 및 관리는 개발자가 직접 담당해야 한다. 이를 통해 리소스의 가용성, 안정성, 준비 상태는 플랫폼에서 보장하지만 프로비저닝 및 관리는 개발자가 직접해야 한다.

------

# 결론

클라우드 컴퓨팅의 현재 상황 및 Google Cloud Platform과 컴퓨팅 리소스에 대해 알아보았다. 클라우드 컴퓨팅의 사용 분야 및 규모는 점점 커지고 있고, 이를 사용하여 개발하는 인력의 규모 또한 커질 것이다. AWS나 Azure 같은 클라우드 서비스도 있지만, 레퍼런스를 통해 깔끔하고 정리된 클라우드 시스템를 배우기엔 GCP가 더 낫다고 생각한다. 또한 스타트업이나 창업을 하려할 때, 클라우드 컴퓨팅 서비스를 활용하여 적은 초기 비용으로 제품을 빠르게 시장에 낼 수 있다는 장점이 있다. Google App Engine이나 Firebase 같은 PaaS 리소스를 배우고 개발함으로 많은 인원이 필요없이 적은 인원이 쉽게 앱을 관리할 수 있으므로 GCP를 사용할 것을 권장한다.

# Reference

AWS Cloud Computing 소개

- https://aws.amazon.com/ko/what-is-cloud-computing/

Gartner Forecasts Worldwide Public Cloud Revenue to Grow 17.3 Percent in 2019

- https://www.gartner.com/en/newsroom/press-releases/2018-09-12-gartner-forecasts-worldwide-public-cloud-revenue-to-grow-17-percent-in-2019

Cloud Service Spending Still Growing Almost 40% per Year; Half of it Won by Amazon & Microsoft

- https://www.srgresearch.com/articles/cloud-service-spending-still-growing-almost-40-year-half-it-won-amazon-microsoft

GCP Wikipedia

- https://ko.wikipedia.org/wiki/구글_클라우드_플랫폼

GCP 개요

- https://cloud.google.com/docs/overview/

Kubernetes 개요

- https://kubernetes.io/ko/docs/concepts/overview/what-is-kubernetes/