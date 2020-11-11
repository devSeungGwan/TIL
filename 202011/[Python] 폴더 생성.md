# [Python] 폴더 생성

## 목적

프로그래밍을 하지 않는 직원 분이 1~158번까지 폴더를 생성하려고 하였다. 일일히 만들려고 하길래 간단하게 폴더를 생성하는 Python 코드를 작성하려고 한다.

## 코드

python 내장 라이브러리인 `os`를 사용한다. `os`에는 라이브러리 이름 그대로 OS에서 작업해야 하는 기능들을 파이썬에서 사용할 수 있도록 해준다.

`os.makedirs(directory)`를 사용하여 directory  위치에 폴더를 생성한다.

```python
import os

for i in range(1, 159):
    directory = "./{}".format(i)
    # 중복 폴더 생성 방지를 위한 Try-Catch
    try:
        if not os.path.exists(directory):
            os.makedirs(directory)
    except OSError:
        print("error!")
```

## 결론

노가다도 좋은 방법이지만, 코드를 통해 해결할 수 있는 것은 많으므로 이러한 접근 위주로 해야 한다.

## Reference

[Python] 파이썬으로 폴더 생성하기 - os.makedirs ([Link](https://data-make.tistory.com/170))