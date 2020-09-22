Node.js 및 NPM(Node Package Manager)의 버전을 관리할 수 있도록 만든 프로그램이다.

**설치는 다음과 같이 진행한다.**

1. Install 및 Update 시 cURL 및 Wget 둘 중 하나를 선택해서 설치한다.

- cURL로 설치

  ```
  curl -o- <https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh> | bash
  ```

- Wget로 설치

  ```
  wget -qO- <https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh> | bash
  ```

  1. .bashrc에 적용한다.

     ```
     source ~/.bashrc
     ```

  2. 정상적으로 설치 되었는 지 확인한다.

     ```
     nvm --version
     ```

# Node.js 및 NPM 설치

NVM을 사용하여 Node.js 및 NPM(Node Package Manager)을 설치한다. NVM으로 Node.js를 설치하기 전에 프로그램 충돌을 피하기 위해 기존에 있던 Node.js는 제거한다.

Node.js를 설치하기 위한 NVM 명령어는 다음과 같다.

```
nvm install "nodeJS Version 입력"
```

Node.js는 LTS(Long Term Service) 버전과 Stable 버전으로 나뉜다. 서버와 같이 안정적인 서비스를 요구할 때는 LTS 버전을 주로 사용하고 Front-End 개발 시에는 Stable 버전을 사용한다.

Node.js 및 NPM 버전을 변경하기 위한 명령어는 다음과 같다.

```
nvm install #write_nodejs_version
```

프로그램이 정상적으로 설치되었는 지 확인한다.

```
node -v
npm -v
```

# Reference

NVM

- https://github.com/nvm-sh/nvm

Node.js Download

- https://nodejs.org/ko/download/

Node.js & NPM 설치

- https://d2fault.github.io/2018/04/30/20180430-install-and-upgrade-nodejs-or-npm/