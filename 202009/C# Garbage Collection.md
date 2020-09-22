물체에 대한 비전 검사 프로그램을 테스팅할 수 있도록 만드는 작업을 진행 중이다. 비전 검사를 진행하면서 사용하는 많은 양의 이미지 데이터들을 배열에 저장하기 위해 사용하는 메모리는 기하급수적으로 늘어난다. 이미지 데이터로 인해 적제되는 메모리를 관리하기 위해 C#에서 제공하는 `Garbage Collection, 이하 GC` 메소드를 사용한다.

`GC` 를 사용하면서 배우고 겪은 내용들을 이번 페이지에 정리하려고 한다.

# GC, Garbage Collection

**메모리 관리 기법 중의 하나로, 프로그램이 동적으로 할당했던 메모리 영역 중에서 필요없게 된 영역을 해제하는 기능이다.** - 위키백과

## 장점

GC는 다음과 같은 버그들을 방지할 수 있다.

- 유효하지 않은 포인터 접근(이미 해제된 메모리에 접근하는 버그)
- 이중 해제(이미 해제된 메모리를 또 다시 해제하는 버그)
- 메모리 누수(더 이상 필요하지 않은 메모리가 해제되지 않고 남아있는 버그)

## 단점

- 어떤 메모리를 해제할 지 결정하는 데 비용이 든다.
- GC가 일어는 타이밍이나 점유 시간을 미리 예측하기 힘들다.
- 할당된 메모리가 해제되는 시점을 알 수 없다.

Garbage Collection에서 Garbage는 불필요한 메모리, 즉 '정리되지 않은 메모리', '유효하지 않은 메모리 주소'를 말한다.

`C`나 `C++`에서는 프로그래머가 프로그램 실행 시 불필요한 메모리를 직접 delete나 free를 통해 해제여 메모리를 확보했다. 프로그래머가 직접 메모리를 해제할 때. 메모리 할당 및 해제가 잦아지거나, 메모리 크기가 작아질 수록 메모리 조각 현상이 빈번하게 일어나게 되고, 메모리 관리에 어려움을 겪게 된다.

하지만 `Java`나 `C#`의 경우 GC을 사용하여 객체가 참조하고 있지 않은 메모리들을 해제할 수 있는 메소드를 제공하고 있다.

GC 특정 조건을 만족하는 상황이 발생하면 **현재 수행중인 Thread들을 모두 중단(Stop-The-World)**시키고 GC Thread를 활성화한다. GC Thread는 힙 상에서 사용 중인 객체 참조 그래프를 생성하고 사용 중인 객체의 위치를 재조정함으로써 사용하지 않는 객체들을 모두 힙상에서 제거한다.

GC가 객체 참조 그래프를 생성하기 위해선 루트 참조가 필요하다.

루트 참조에 해당하는 것들

- 현재 각 쓰래드가 수행중인 메서드의 로컬 변수(스텍 변수)
- CPU 레지스터 변수가 가지고 있는 참조
- 현재 사용중인 각 타입(클래스)의 정적 필드(Static Field)
- 전역 변수(Global Variable)

각 루트 참조가 참조하는 객체, 그리고 다시 그 객체가 참조하는 다른 객체들을 참조 그래프에 추가함으로써 현재 사용중인 객체의 그래프를 작성한다. 객체 참조 그래프가 완성되면 이 그래프에 포함되지 않은 모든 객체는 객체에 대한 참조가 존재하지 않는 객체가 되며 GC의 대상이 된다. GC를 실행할 때 메모리 컴팩션을 수행하게 되는데, 참조 그래프 상의 객체들을 힙 상에서 재배치하고 메모리 할당 포인터를 감소시킴으로써 GC를 수행한다.

# GC Methods

### [GC.Collect(](https://docs.microsoft.com/ko-kr/dotnet/api/system.gc.collect?view=netframework-4.8))

- 모든 세대(0~2세대)의 Garbage Collection을 즉시 수행한다.
- GC를 실행할 세대 지정 및 강제 실행 지정, 백그라운드 GC 차단, 메모리 압축에 대한 파라미터를 제공한다.

### [GC.CollectionCount(int 32)](https://docs.microsoft.com/ko-kr/dotnet/api/system.gc.collectioncount?view=netframework-4.8#System_GC_CollectionCount_System_Int32_)

- 지정된 세대에 대한 GC 수행 횟수를 반환한다.

# ISSUE

## 힙손상

`GC.Collect()` 를 코드에 추가하고 테스트 프로그램을 돌릴 때, `[0xc0000374](<https://www.google.com/search?sxsrf=ACYBGNSfT0MjvhvTUiRzXdc2fhbREONIvQ:1581317942896&q=0xc0000374&sa=X&ved=2ahUKEwjAo42ytMbnAhWJH3AKHRB3BYgQ1QIoAnoECAsQAw&cshid=1581318073145566&biw=1278&bih=925>)` 에러를 던지며 런타임이 종료되는 것을 볼 수 있었다. 이 에러를 구글링하니 힙손상이라는 이슈를 발견할 수 있었다.

기존 코드에서 힙손상(Heap Corruption)이 발생한 이유는 `GC.Collect()` 를 사용하여 메모리가 해제된 객체를 참조가 발생하여 에러가 발생하였다. 즉, 없는 객체를 참조했기 때문에 힙 손상이 일어났다.  `GC.Collect()`가 메모리를 돌면서 초기화해야하는 객체까지 메모리를 해제하였다. 프로그램 내 사용되는 변수를 최대한 적게 할당함으로 GC를 최대한 적게쓰는 방향으로 프로그래밍을 진행하였다.

# 마치며

GC를 프로그램에 적용시키며 필요했던 지식이나 이슈를 정리해서 이 글을 포스팅했다. 메모리를 자동으로 정리해주는 기능은 메소드 한줄만 사용해도 손쉽게 사용이 가능하다. 하지만 메모리를 건드리는 작업이기 때문에 힙손상 등 Critical Error가 뜰 가능성이 있으므로 GC에 대한 개념을 확실하게 알고 사용해야 적재적소에 사용할 수 있고, 메모리와 관련된 이슈를 피할 수 있다.

# Reference

- Garbage Collection
  - https://ko.wikipedia.org/wiki/쓰레기_수집_(컴퓨터_과학)
- 닷넷 가비지 컬렉션 다시 보기 - Part I
  - http://www.simpleisbest.net/post/2011/04/01/Review-NET-Garbage-Collection.aspx
- 힙 손상 탐지(1) - 초기화 안 된 상태로 사용
  - https://nightohl.tistory.com/entry/힙-손상-탐지1-초기화-안-된-상태로-사용
- 가비지 컬렉터(GC)에 대하여
  - https://velog.io/@litien/가비지-컬렉터GC
- Java Garbage Collection
  - https://d2.naver.com/helloworld/1329
- Java Reference와 GC
  - https://d2.naver.com/helloworld/329631
- Garbage Collection 모니터링 방법
  - https://d2.naver.com/helloworld/6043
- Garbage Collection 튜닝
  - https://d2.naver.com/helloworld/37111