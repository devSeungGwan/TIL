`C#`에서 제공하는 예외처리 방식 및 디버깅하다가 찾아본 예외들의 발생 과정, 해결 방안 등을 설명한다.

# 예외 처리(Exception)

# 이 때까지 만났었던 예외처리 목록

## Mysql.Data.MysqlClient.MysqlException

- 설정값이 저장되어 있는 Mysql에 프로시져를 사용해 C# 객체로 매핑하는 과정에서 예외가 발생하였다.
- `MysqlConnection` 클래스를 사용하여 외부 서버에 있는 `Mysql`과 연결 중 예외 발생 시 출력된다.
- 출력 목록
  - Message: 현재 발생한 Exception을 설명하는 메시지
  - Number: 어떤 에러로 예외처리가 되었는 지 확인할 수 있는 에러 번호

## System.Exception(OpenCVSharp.dll)

- 현재 프로젝트에서 기존에 사용되던 OpenCV Lagacy Code 때문에 예외처리가 발생되었다.
- OpenCV4에서 OpenCV3-anyCPU(기존 프로젝트 사용 버전)으로 다운그래이드 함으로 예외를 회피하였다.

## [System.NullReferenceException](https://docs.microsoft.com/ko-kr/dotnet/api/system.nullreferenceexception?view=netframework-4.8): '개체 참조가 개체의 인스턴스로 설정되지 않았습니다.'

- 객체에 `Null` 값이 할당될 때 다음과 같은 예외처리가 발생하였다.
- Null 예외 처리를 하여 해결 가능하다.

## [Exception from HRESULT: 0x800A03EC](https://nsinc.tistory.com/125)

- 엑셀에 값을 대입할 때 맞지 않는 `[row, col]`  값을 대입해주어 예외처리가 발생하였다.
- 엑셀은 `[row, col]` 이 `[1, 1]` 부터 시작하므로 0이나 엑셀에 최대로 넣을 수 있는 `[row, col]` 값을 넣지 않도록 한다.

## System.InvalidOperationException'(WindowsBase.dll)

- Thread 환경에서는 WPF UI Thread에 직접 접근이 불가능하여 이러한 예외처리가 발생하였다.
- `Dispatcher.Invoke(DispatcherPriority.Normal, New Action(delegete()))` 를 사용하여 WPF 내 UI를 동적으로 수정할 수 있다.

## [System.IndexOutOfRangeException: '인덱스가 배열 범위를 벗어났습니다.'](https://docs.microsoft.com/ko-kr/dotnet/api/system.indexoutofrangeexception?view=netframework-4.8)

- 리스트가 현재 가지고 있는 최대 크기를 넘는 인덱스를 참조해서 발생하였다.
- 리스트에 요소를 추가할 때 어떤 이유로 리스트에 요소가 추가가 안된 상황이 발생했다. 이후 다른 곳에서  추가가 안된 리스트를 불러와 해당 위치의 요소를 사용할 때 주로 발생한다.
- 사용하려는 리스트에서 데이터의 추가가 올바르게 이루어지고 있는 지 확인한다.

## [예외 발생: 'System.ArgumentOutOfRangeException'(mscorlib.dll)](https://docs.microsoft.com/ko-kr/dotnet/api/system.argumentoutofrangeexception?view=netframework-4.8)

- 메소드에 사용되는 파라미터가 잘못되어 발생하는 예외이다.
- 이 예외는 개발자 문제라고 MSDN에 정확하게 명시되어 있고, 레퍼런스가 잘 되어 있어서 위 링크를 참고하여 상황에 맞는 해결방법을 획득하는 것이 좋다.