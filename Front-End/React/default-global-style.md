# 스타일 설정

## 초기화 라이브러리(styled-reset)

Eric Meyer 스타일 초기화 라이브러리

```
npm i styled-reset
```

## 글로벌 스타일에 적용(styled-components)

```
npm i styled-components
```

```jsx
// src/styles/GlobalStyles.js

import { createGlobalStyle } from "styled-components";
import reset from "styled-reset";
const GlobalStyles = createGlobalStyle`

${reset}  
/* Eric Meyer에 추가로 자주 사용하는 초기 설정 */
/* https://github.com/CSH111/TIL/blob/master/Front-End/css/reset.md */


/* 글꼴 등 추가 설정 */

`;

export default GlobalStyles;
```

뿌려주기(App에 뿌려도 ㄱㅊ)

```jsx
//index.js

...
import GlobalStyles from "./styles/GlobalStyles";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
    <>
      <GlobalStyles />
      <App />
    </>
);

```
