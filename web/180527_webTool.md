### 초프개7주차
---

- babel : es6문법을 ie에서 사용할 수 있도록 변환해주는 툴
```
- 설치는 터미널에서
npm install --save-dev babel babel-cli

- 설정
 패키지.json에서 추가 build를 추가함. 
   "scripts": {
    "build": "babel src --out-dir lib",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  babel src --out-dir lib
src에 있는 파일을 lib파일에 생성해준다


- 실행 터미널에서 명령어
npm run build  

이렇게만 하면 새로운 파일만 뽑아낼 뿐 es6문법이 5문법이 되지는 않는다

- 추가 플러그인 설치, 터미널에서
npm i -D babel-preset-env 을 설치해준다.

----------------------
install  ->  i로 축약
--save-dev  -> -D로 축약
----------------------


설치만 해서는 es6문법이 es5문법으로 변환하지 않는다.

프로젝트 폴더 바로 아래에 .babelrc 파일을 만든다
객체형태로
{
  "presets": [
    ["env"]
  ]
}

를 적어준다.

그 후 다시 npm run build 실행하면 lib폴더의 js가 es5문법으로 변경되어있다


    "build": "babel src --out-dir lib", //한번만 빌드됨
    "build:watch": "babel src --out-dir lib --watch", //저장할때마다 계속 빌드됨
```
웹팩설치 이전은   
소스 -> 바벨 -> 빌드 -> 브라우저

- webpack

``
웹팩설치 
npm i -D webpack webpack-cli

웹팩과 바벨의 구동

소스 -> 웹팩 -> 빌드 -> 브라우저
        | | ->바벨로더
     -> 바벨

``

웹팩과 바벨이 통신할수 있는 것 - 바벨로더가 필요하다
웹팩설정파일에 바벨로더를 설정한다고 되는게 아니라 바벨로더를 설치해야한다