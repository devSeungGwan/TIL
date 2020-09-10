# 목적

GitHub Action을 통하여 AI Edge 개발 및 배포 파이프라인을 개선한다. 이를 하기 위한 기반 지식들을 적기 위한 문서이다.

# GitHub Action

소프트웨어의 `Workflow(Test, CI/CD, etc...)`를 자동화할 수 있도록 도와주는 도구이다. `GitHub` 내에서 실행이 가능하고, 테스트 및 빌드를 쉽게하고 결과를 진단받을 수 있다.

## 구성 요소

### Workflow

* 여러 Job으로 구성되고, Event에 의해 트리거 될 수 있는 자동화된 프로세스
* 최상위 개념
* `Workflow` 파일은 `YAML`으로 작성되고, `GitHub Repository` 내 `./github/workflows` 폴더에 저장된다.

### Event

* Workflow를 Trigger(실행)하는 특정 활동이나 규칙
* 다음같은 상황에서 사용가능
  * 특정 브랜치에 Push/Pull Request
  * 특정 시간대에 반복(Cron)
  * Webhook을 사용해 외부 이벤트에 알림 및 실행

### Job

* Job은 여러 Step으로 구성되고, 가상 환경의 인스턴스에서 실행된다.
* 다른 Job에 의존 관계를 가질 수 있고, 독립적으로 병렬 실행도 가능하다.

### Step

* Task들의 집합으로, 커맨드를 날리거나 Action을 실행할 수 있다.

### Action

* Workflow의 가장 작은 블록(Smallest portable building block)
* Job을 만들기 위해 Step들을 연결할 수 있음
* 재사용이 가능한 컴포넌트(상속 가능)
* 개인적으로 만든 Action을 사용할 수도 있고, Marketplace에 있는 공용 Action을 사용할 수도 있다.

### Runner

* GitHub Action Runner 어플리케이션이 설치된 머신으로, Workflow가 실행될 인스턴스
* GitHub에서 호스팅해주는 GitHub-hosted runner와 직접 호스팅하는 Self-hosted runner로 나뉜다.
* GitHub-hosted runner는 Azure의 Standard_DS2_v2로 vCPUI 2, 메모리 7GB, 임시 스토리지 14GB가 제공된다.
* Self-hosted runner는 다음 [문서](https://docs.github.com/en/actions/hosting-your-own-runners/adding-self-hosted-runners)를 참조한다.

## Workflow 정책

Workflow는 하나의 Repository에 최대 20개까지 등록이 가능하다.

Workflow 내에 존재하는 Job은 6시간동안 실행될 수 있고, 초과 시 자동으로 중지된다.

## 가격 정책

|           | Free         | Pro                | Team                | Enterprise  |
| --------- | ------------ | ------------------ | ------------------- | ----------- |
| Storage   | 500 MB       | 1 GB               | 2 GB                | 50 GB       |
| 실행 시간 | 2,000 시간   | 3,000 시간         | 3,000 시간          | 50,000 시간 |
| 가격      | 0 /per month | $ 4 per user/month | $ 21 per user/month | 문의        |

# YAML

Yet Another Markup Language(구), YAML Ain't Markup Language 라고 불리며, 말 그대로 마크업 언어가 아닌, 사람이 읽을 수 있는 데이터 `Serialization` 표준이다.(Human-readable data serialization language) 

파이썬 문법처럼 개행을 통해 구조체를 구성하며, `JSON`이 `YAML`의 부분 집합이므로, `YAML` 파서는 `JSON`을 읽을 수 있다. 주석은 `#`으로 처리한다. 

다중 컨테이너 구성 요소를 정의하여 빌드할 수 있는 도구인 `Docker Compose` 나 `Container Deployment` 를 위한 도구인 `Kubernetes` 등에 사용된다.

JSON 처럼 Map 구조를 지원하고 상속(Inherit) 을 지원한다.

# CI/CD

## 정의

![Image for post](https://miro.medium.com/max/625/1*4UtNE2uAl37bl_FmIafl6A.png)

> 그림 1. CI/CD 과정

애플리케이션 개발 단계를 자동화하여 애플리케이션을 보다 짧은 주기로 고객에게 제공하는 방법

새로운 코드의 통합으로 인하여 개발 및 운영팀에 발생하는 문제를 해결하는 솔루션이다.

## 배경

* 소프트웨어가 거대해지고 복잡해지면서, 팀 단위로 개발하게 되었고, 그 과정에서 분업과 협업은 필수가 되었다. 이 분업과 협업의 과정에서 코드의 Merge 과정은 매우 까다롭고, 테스트하는데 큰 자원을 소비하게 된다. 이 문제를 해결하기 위해 도입되었다.
* 개발 브랜치가 일정 기간 이상 이용되면, 통합의 어려움은 커지고 충돌 해결에 들어가는 시간이 길어지고 오류 발생 위험이 커진다. 이러한 단점을 극복하고자 변동 내용의 반영 빈도를 늘리는 자동화가 등장되었다.
* 빌드와 기능성을 검증하는 새로운 방법을 확보하고 기능의 개발과 배치 속도를 큰 폭으로 개선하기 시작하였다.

## CI(Continuous Integration, 지속적 통합)

* Build & Packaging
* 새로운 코드 변경 사항이 정기적으로 빌드 및 테스트되어 공유 리포지토리에 병합되는 것이다.
* Build, Test를 실시하는 프로세스를 말하며, 이러한 통합 프로세스를 상시 실시하는 것이다.
* 다수의 개발자가 동시에 애플리케이션 개발과 관련된 코드 작업을 할 경우, 서로 충돌할 수 있는 문제를 해결하기 위함이다.
* 언제든 최신 Build를 고객에게 바로 제공 가능하게 한다.

## CD(Continous Delivery, Continous Deployment, 지속적인 서비스 제공, 지속적인 배포)

* 개발자들이 애플리케이션에 적용한 변경 사항이 버그 테스트를 거쳐 리포지토리에 자동으로 업로드되는 것이다.
* 개발자의 변경 사항을 리포지토리에서 고객이 사용가능한 프로덕션 환경까지 자동으로 릴리스하는 것이다.
* 해당 리포지토리에서 애플리케이션을 실시간 프로덕션 환경으로 배포된다.
* 개발팀과 운영팀의 커뮤니케이션 문제를 해결한다.

## 필요성

* 모든 분기의 소스코드를 병합하는 경우, 결과적으로 반복적인 수작업에 많은 시간이 소요된다.
* 병합합는 수작업을 하지 않는다면, 개발자가 애플리케이션에 변경 사항을 적용할 때, 다른 개발자가 동시에 적용하는 변경 사항과 충돌(Comflict)을 이르킬 수 있다.
* 자동화된 테스트에서 기존 코드와 신규 코드 간의 충돌이 발견되면 CI를 통해 이러한 버그를 더욱 빠르게 자주 수정할 수 있다.
* 여러 사람과 작성한 코드가 병합되었을 때 생기는 문제를 미리 감지한다.
*  System과 Application을 최대한 최신 상태로 유지할 수 있다.

# 참조

## Github Action

https://github.com/features/actions

https://docs.github.com/en/actions

https://zzsza.github.io/development/2020/06/06/github-action/

[깃허브의 액션 기능을 사용해보자](https://medium.com/@elastic7327/%EA%B9%83%ED%97%88%EB%B8%8C%EC%9D%98-%EC%95%A1%EC%85%98-%EA%B8%B0%EB%8A%A5-git-action-%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%B4%EB%B3%B4%EC%9E%90-ed634d622280)

## GitHub Action Billing Plan

https://github.com/pricing#github-one

https://docs.github.com/en/github/setting-up-and-managing-billing-and-payments-on-github/about-billing-for-github-actions

## CI/CD

https://medium.com/@hoi5088/ci-cd-%EA%B0%9C%EB%85%90-4e6a45dbcfe2

https://ko.wikipedia.org/wiki/%EC%A7%80%EC%86%8D%EC%A0%81_%ED%86%B5%ED%95%A9

https://ko.wikipedia.org/wiki/%EC%A7%80%EC%86%8D%EC%A0%81_%EB%B0%B0%ED%8F%AC

## Yaml

https://johngrib.github.io/wiki/YAML/

https://www.inflearn.com/questions/16184

https://perfectacle.github.io/2018/08/19/yaml/

## Docker Compose

https://hoony-gunputer.tistory.com/entry/docker-compose-yaml-%ED%8C%8C%EC%9D%BC-%EC%9E%91%EC%84%B1

## Kubernetes

https://kubernetes.io/ko/docs/concepts/overview/what-is-kubernetes/