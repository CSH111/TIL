# pages 폴더 구조의 예시(index 이용)

## 폴더내부의 index.js

폴더 내부에 index.js 가 있으면 외부에서 해당폴더에서 바로 index.js가 export 하고있는 것을 import 할 수 있다.

```
폴더구조 예시

my project
│
│── Pages
│      │── index.js
│      │── Login
│      │     │── index.js
│      │     └── loginForm.js
│      └── Home
│            │── index.js
│            └── Notice.js
│── App.js
│──
│──
```

```jsx
// Login/index.js (login폴더 내부의 index.js)

import LoginForm from "./LoginForm";

const Login = () => {
  return (
    <>
      <h1>로그인페이지</h1>
      <LoginForm />
    </>
  );
};

export default Login; //Login 컴포넌트(페이지) export
```

```jsx
// /pages/index.js  (pages폴더 내부의 index.js)

import Home from "./Home";
import Login from "./Login";
//폴더로 접근하면 바로 index.js 내부에 접근 할 수 있다.

export { Home, Login }; //page들을 모아서 한번에 export
```

```jsx
// App.js

import { BrowserRouter, Route, Routes } from "react-router-dom";
import { Home, Login } from "./pages";
//페이지 폴더로 접근해서 한번에 import

export function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/login" element={<Login />} />
      </Routes>
    </BrowserRouter>
  );
}
```

이점

- app에서 import 간소화

  ```jsx
  // before
  import Home from "./pages/Home/Home.js";
  import Login from "./pages/Login/Login.js";

  //after
  import { Home, Login } from "./pages";
  ```
