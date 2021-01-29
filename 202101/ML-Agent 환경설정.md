## 준비물

1. `Git`
   * Git 명령어를 사용하기 위한 프로그램 다운로드

```url
https://git-scm.com/
```

2. Unity ML-Agents Release 12를 CMD를 사용하여 원하는 경로에 Clone한다.

```sh
$ git clone --branch release_12 https://github.com/Unity-Technologies/ml-agents.git
```

3. `Anaconda`(Python)

```url
https://www.anaconda.com/products/individual#Downloads
```

* 설치 이후 설치가 잘되었는 지 확인한다.

```shell
conda -V
```

> conda 4.8.3

⚠️ 아나콘다를 설치했는데 다음 명령어가 없다고 나오면, `아나콘다 환경변수`가 설정이 되지 않은 것임.

![image-20210129160544771](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20210129160544771.png)

🛠 Add Anaconda to my PATH environment variable 을 체크 후 아나콘다를 설치하면 윈도우 환경변수에 아나콘다 환경을 추가하여 설치해준다.

4. `Unity`



## 파이썬 환경설정

1. Anaconda 설치 후 CMD 창을 연다.
2. `mlagent` 설치

```sh
pip install mlagents=0.23.0
```

3. pytorch 설치

```sh
pip3 install torch==1.7.0 -f https://download.pytorch.org/whl/torch_stable.html
```



## 유니티 프로젝트 생성

ML-Agents를 사용하기 위한 새로운 유니티 프로젝트를 생성한다.



## Unity ML-Agent 적용

생성한 유니티 프로젝트에 ML-Agents Release 12 버전의 com.unity.ml-agents 롤더 패키지를 통해 설치 진행

1. Unity > Window > Package Manager
2. Package Manager 내 + 버튼을 클릭한다.
3. Add package from disk 를 클릭한다.
4. com.unity.ml-agents 폴더를 찾는다.
5. package.json 폴더를 클릭한다.



## ML-Agents 예제 프로젝트 

https://github.com/Unity-Technologies/ml-agents/blob/master/docs/Learning-Environment-Create-New.md