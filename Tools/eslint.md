# eslint

eslint는 코드스타일을 일관되게 작성할 수 있도록 안내해주는 패키지.  
팀프로젝트시 유용.

## 리액트에서 사용해보며 개념익히기

- CRA 이용시 eslint는 설치되어있음

### config 도우미

```
npm init @eslint/config
```

실행시 여러가지 물음에 대한 답변에 따라 적당한 config file을 만들어줌.  
모든 물음에 답하면 root 경로에 `eslintrc`파일이 생성되어있음

```js
// .eslintrc.js

module.exports = {
  env: {
    //실행환경
    browser: true,
    es2021: true,
    node: true, // module을 찾을 수 없다고하면 node입력
  },
  extends: ["eslint:recommended", "plugin:react/recommended"],
  // extends는 사용할 플러그인과 룰이 함께 저장되어있는 패키지임
  // npm 으로 설치해서 사용.

  overrides: [],
  parserOptions: {
    ecmaVersion: "latest",
    sourceType: "module",
  },
  plugins: ["react"],
  //플러그인은 해당 플러그인에서 정의되어있는 룰을 사용할 수 있게끔 해줌
  // 룰을 비워둔다면 아무일도 일어나지않음
  // npm 으로 설치해서 사용

  rules: {
    "react/react-in-jsx-scope": "off",
  },
  //룰은 플러그인에 정의되어있는 룰을 직접입력해서 사용하는곳
  // extends로 한번에 설정한 옵션중 마음에 안드는 부분을 수정하거나
  // 새로운 룰을 추가해서 이용할 수 있따.
  // 물론 extends없이 하나하나 내맘대로 입력해서 사용할 수 있다.
  // extends에서 사용하고 있는 플러그인에 대한 룰이라면 별도로 플러그인을 입력하지 않아도 룰을 입력가능한 것처럼 보이는데 체크해보기..
};
```

<br>

## 자주사용되는 extends, plugin

<br>

### eslint-config-prettier

- eslint 에서는 프리티어 처럼 포맷을 설정해주는 옵션들이 있다.
- 해당 부분이 사용자의 프리티어와 충돌하지 않게끔 포맷팅 기능을 꺼주는 패키지

```
npm i -D eslint-config-prettier
```

```js
// .eslintrc.js

extends: ["eslint-config-prettier"]
extends: ["prettier"] //혹은 축약사용가능
```

<br>

### eslint-plugin-simple-import-sort

- import export 구문들을 정렬하게끔 표시해주는 eslint 패키지
- eslint-plugin-import 라는 패키지의 order기능이 있지만 이게 더 간편해보인다.

```
npm i -D eslint-plugin-simple-import-sort
```

```js
// .eslintrc.js
 plugins: ["simple-import-sort"],
   rules: {
    "simple-import-sort/imports": "error",
    "simple-import-sort/exports": "error",
   }
```

```js
// setting.json  - vscode 환경설정

 "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },

  //저장시 마다 "simple-import-sort" 룰에 맞춰 정렬해준다.
```
