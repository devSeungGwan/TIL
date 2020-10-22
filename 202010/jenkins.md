# 개요

소프트웨어 개발 이후 배포 자동화(CI/CD) 도구인 Jenkins에 대해 알아본다. 

젠킨스는 거의 모든 언어에 대한 소스코드 리포지토리에 대한 지속적인 통합과 지속적인 전달 환경을 구축하기 위한 간단한 방법을 제공한다.

다수의 개발자들이 하나의 프로그램을 개발할 때 버전 충돌을 방지하기 위해 각자 작업한 내용을 공유영역에 있는 저장소에 빈번히 업로드함으로써 지속적 통합을 가능하도록 해준다.

젠킨스가 각각의 단계에 대한 스크립트 작성에 대한 필요성을 없애주진 않지만, 빠르고 강력하게 빌드, 테스트, 그리고 배포 도구등 체인 전체를 통합할 수 있는 방법을 제공해준다.

# 역사

2004년에 코스케 가와구치는 썬의 자바 개발자였다. 가와구치는 개발 작업에서 빌드를 깨는 것에 질려서, 코드를 리포지토리에 커밋하기 전에 해당 코드의 동작 여부를 알 수 있는 방법을 찾고 싶었다.그래서 가와구치는 이를 가능케하는 자동화 서버를 자바로 개발했고, 허드슨이라는 이름을 붙였다. 허드슨은 썬에서 유명해졌으며, 오픈소스로 다른 기업들에게 확산되었다.

2011년으로 접어들면서, 오라클 그리고 독자적인 허드슨 오픈소스 커뮤니티 간의 분쟁으로 젠킨스라는 새로운 이름을 달고 갈라지게 되었다. 두 분류 모두 존속했지만, 젠킨스가 훨씬 더 활동적이였다. 2014년에 가와구치는 젠킨스 기반의 지속적 배포 제품을 공급하고 있는 클라우드 비즈의 CTO가 되었다.

# 장점

개발중인 프로젝트에서 커밋은 매우 빈번히 일어나기 때문에 커밋 횟수만큼 빌드를 실행하는 것이 아니라 작업이 큐잉되어 자신이 실행될 차례를 기다리게 된다.

코드 변경과 함께 이뤄지는 자동화된 빌드 및 테스트 작업들은 다음과 같은 이점들을 가져다 준다.

* 프로젝트 표준 컴파일 환경에서 컴파일 오류 검출
* 자동화 테스트 수행
* 정적 코드 분석에 의한 코딩 규약 준수여부 체크
* 프로파일링 툴을 이용한 소스 변경에 따른 성능 변화 감시
* 결합 테스트 환경에 대한 배포 작업

* 플러그인 인스톨을 통한 기능 추가
* 스크립트(파이썬)을 이용한 기능 추가

## 각종 배치 작업의 간략화

프로젝트 기간 중에 개발자들은 순수한 개발 작업 이외에 DB 셋업이나 환경설정, 배포 작업과 같은 단순 작업에 시간과 노력을 들이는 경우가 빈번하다. 

DB 구축, 어플리케이션 서버 배포, 라이브러리 릴리즈 같이 이전에 CLI로 실행되던 작업들을 쉽게 진행할 수 있다.

## Build 자동화의 확립

빌드 툴의 경우 Java는 Maven과 Gradle이 자리잡고 있으며, 이미 빌드 관리 툴을 이용해 프로젝트를 진행하고 있다면, 젠킨스를 연동하여 빌드 자동화를 통해 프로젝트 진행의 효율성을 높힐 수 있다.

## 자동화 테스트

젠킨스를 사용해야 하는 가장 큰 이유 중 하나이며, 사실상 자동화 테스트가 포함되지 않은 빌드는 CI 자체가 불가능하다고 봐도 무방하다. 

젠킨스는 SVN이나 Git과 같은 버전관리시스템과 연동하여 코드 변경을 감지하고 자동화 테스트를 수행하기 때문에 만약 개인이 지나친 테스트가 있더라도 젠킨스 선에서 테스트를 진행해준다.

## 코드 표준 준수여부 검사

코드 품질 검사를 빌드 내부에서 수행함으로써 기술적 부재의 감소도 크게 기여한다.

## 빌드 파이프라인 구성

2개 이상의 모듈에서 구성되는 레이어드 아키텍처가 적용된 프로젝트에는 그에 따른 빌드 파이프라인 구성이 필요하다.

도메인 ->서비스->UI 와 같이 각 레이어의 참조 관계에 따라 순차적으로 빌드를 진행하지 않으면 안된다. 젠킨스에선 이러한 빌드 파이프라인의 구성을 간단히 할 수 있으며, 스크립트를 통해 복잡한 제어도 가능하다.

# Reference

[Jenkins\] 젠킨스란 무엇인가](https://ict-nroo.tistory.com/31)

[젠킨스란 무엇인가, CI(Continuous Integration) 서버의 이해![img](http://linkback.itworld.co.kr/images/onebyone.gif?action_id=99b3d792f06da6f985904f1bb39b216)](http://www.itworld.co.kr/news/107527#csidx99b3d792f06da6f985904f1bb39b216)
