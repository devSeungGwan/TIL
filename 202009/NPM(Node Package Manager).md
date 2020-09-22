- **NPM(Node Package Manager)**은 JavaScript 런타임 환경인 Node.js 에서 사용하는 모듈들을 패키지화 하여 다운 및 관리해주는 프로그램이다.
- NPM을 통해 다른 사람들이 개발한 패키지를 다운받아 사용함으로써 개발 속도를 가속화 시킬 수 있으며, 반대로 자신이 패키지를 배포하여 손쉽게 공유할 수 있다.
- NPM은 Node.js 설치 시 자동으로 설치가 되며 설치 방법은 이전 게시글(https://www.notion.so/seunggwan/Node-js-eb5767a2af654019898facfb8ed92887)에서 확인할 수 있다.

------

# 설치 및 업데이트

Node.js 패키지 관리를 위해 NVM에서는 Package.json 파일을 생성 후 사용한다. 패키지 목록(Package.json)을 생성 시 다음과 같은 명령어를 사용한다.

```
nvm init
```

`nvm init -y`(default 정보)로 Package.json 생성 시 추가되는 항목은 다음과 같다.

```json
{
  "name": "song",
  "version": "1.0.0",
  "description": "for study",
  "main": "index.js",
  "scripts": {
    "test": "echo \\"Error: no test specified\\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "keywords": []
}
```

- `npm install`

  - Node 패키지를 설치하거나 Package.json을 업데이트 시 사용한다.

  - npm5 버전 이후에는 `--save` 옵션이 default 옵션으로 동작한다.A

  - ```
    —save-dev
    ```

    , 

    ```
    -D
    ```

    - devDependencies에 설치

  - ```
    -g
    ```

    - 글로벌 패키지(시스템)에 설치

  - ```
    npm install package_version
    ```

    - 특정 버전의 패키지 설치

  - ```
    npm install URL
    ```

    - 특정 저장소(Github)에 있는 패키지 설치

- `npm update`

  - 설치한 패키지를 대상으로 업데이트를 할 때 사용한다.

- `npm dedupe`

  - NPM의 중복된 패키지를 정리 시 사용한다.

- `npm version [version]`

  - npm의 버전을 업데이트하거나 변경할 때 사용한다.

------

# 조회

- `npm root`
  - node_module의 위치를 알려준다.
- `npm outdated`
  - 버전이 낮은 패키지를 조회한다.
  - Package.json에 명세된 버전 범위 내에 있을 경우, 빨간색으로 표시하고 아닐 경우 노랑색으로 표시한다.
- `npm ls`
  - 현재 설치된 패키지의 버전 및 Dependencies를 트리 구조로 표현한다.
- `npm ll [package]`
  - 해당 패키지 존재 여부 및 Dependencies를 보여준다.
- `npm search`
  - npm 저장소에서 패키지를 검색한다.
  - 패키지의 이름, 설명, 키워드를 통해 검색 가능
- `npm owner`
  - 패키지의 Author을 검색한다.
  - Author을 설정하거나 삭제할 수 있다.

------

# 로그인

- `npm adduser(npm login)`
  - npm에 회원가입을 할 때 사용한다.
- `npm logout`
  - 로그인 된 npm user을 로그아웃 시킬 때 사용한다.

------

# 출시

- `npm publish`
  - 패키지를 직접 출시하거나 버전 업그래이드를 할 때 사용하고
  - npm에 로그인이 되어야 업로드 가능하다.
  - .gitignore 이나 .npmignore에 적혀있지 않은 파일들은 npm 저장소에 업로드된다.
- `npm deprecate`
  - 패키지나 패키지 내 모듈을 사용하지 않도록 권고한다.
    - 패키지 내 치명적인 버그가 있을 경우
    - 새로운 모듈을 업데이트하여 기존 모듈을 사용하지 않을 때
- `npm unpublish`
  - publish 한 패키지를 철회하여 더 이상 사용하지 못 하도록 한다.
  - deprecate을 사용하여 미리 권고를 한 다음 사용하도록 하여 기존 사용자에게 피해가 최소가 되도록 한다.

------

# 실행

- `npm start`
  - package.json의 scripts에 있는 start 명령어를 실행한다.
  - default
    - `node server.js`
- `npm stop`
  - `npm start` 로 시작한 스크립트를 멈출 때 사용한다.
- `npm restart`
  - `npm stop`  ➡️ `npm start`
- `npm run`
  - Script 내의 다른 명령어를 사용한다.

# 설정

- `npm cache`

  - npm 내의 cache를 보여준다.

  - ```
    npm cache clean
    ```

    - npm의 cache를 초기화한다.

- `npm rebulid`

  - npm을 다시 설치한다.
  - npm에 문제가 생길 경우, `npm cache clean`으로 cache를 삭제하고, `npm rebuild`를 사용하여 재설치한다.

- `npm config`

  - npm을 설정하기 위해 사용한다.

  - ```
    npm config list
    ```

    - npm 내 설정 값을 볼 수 있다.

  - ```
    npm set [name] [value]
    ```

    - 속성을 변경하거나 설정한다.

  - ```
    npm get [name]
    ```

    - 속성을 조회한다.

------

# Reference

https://junwoo45.github.io/2019-07-08-npm/

https://www.zerocho.com/category/NodeJS/post/58285e4840a6d700184ebd87