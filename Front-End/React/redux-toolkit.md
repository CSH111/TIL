# 리액트 리덕스(툴킷)

리덕스 툴킷은 리덕스의 서트파티 라이브러리로 리덕스에서 운영하며 공식적으로 권장되는 리덕스의 사용 툴이다.

<br>

## 0. 패키지 설치

```
npm i react-redux
npm i @reduxjs/toolkit
```

redux 자체는 설치필요 x 툴킷에 패키지에 내장되어있음

<br>

## 1. 개별 슬라이스 생성

```jsx
// src/store/auth.js

import { createSlice } from "@reduxjs/toolkit";

const initailAuthState = {
  isAuthenticated: false,
};

// slice는 리덕스 스토어를 여러개로 분리시켜 관리할 수 있게해준다.
// 초기 상태와 actions를 정의한다
// type별  reducers들을 하나로 통합해 생성해준다. 그걸 export해 store/index 에서 스토어 생성에 이용

const authSlice = createSlice({
  name: "auth",
  initialState: initailAuthState,
  reducers: {
    login(state) {
      state.isAuthenticated = true;
    },
    logout(state) {
      state.isAuthenticated = false;
    },

    //두번째 인자로 사용하는곳으로부터 데이터를 받아올 수있다.
    someFn(state, action) {
      console.log(action.payload); //action.payload에 담겨옴
    },
  },
});

// actions는 스토어에 변경을 줄 곳에서 사용
export const authActions = authSlice.actions;
export default authSlice.reducer;
```

<br>

## 2. 스토어 생성

```jsx
// src/store/index.js

// 사용자가 정의한 개별 slice 들을 임포트 해서 스토어 생성
import { configureStore } from "@reduxjs/toolkit";
import authSliceReducer from "./auth";
import counterSliceReducer from "./counter";

const store = configureStore({
  reducer: { counter: counterSliceReducer, auth: authSliceReducer },
});

export default store;
```

<br>

## 3. 리액트 전역 상태 선언

정의한 스토어를 리액트에 뿌려준다.

```jsx
// index.js

//import ...
import { Provider } from "react-redux";
import store from "./store";

const root = ReactDOM.createRoot(document.getElementById("root"));

root.render(
  <Provider store={store}>
    <App />
  </Provider>
);

// 이제부터 리액트 프로젝트에서 상태 변경 및 가져오기 가능
```

<br>

## 4. 상태 가져오기

```jsx
import { useSelector } from "react-redux";
// useSelector 훅 이용 상태 반영
// isAuthenticated는 개별 슬라이스에서 정의된 상태값

const Header = () => {
  const isLoggedIn = useSelector((state) => state.auth.isAuthenticated);
  // ...

  return (
    <header className={classes.header}>
      {/* ... */}
      {isLoggedIn && <button>Logout</button>}
    </header>
  );
};

export default Header;
```

<br>

## 4. 상태 변경하기

```jsx
import { useDispatch } from "react-redux";
import { authActions } from "../store/auth";
//useDispatch 훅을 이용, 개별slice에서 정의한 actions을 dispatch할 수 있다..

const Auth = () => {
  const dispatch = useDispatch();
  const { login } = authActions;

  const submitHandler = (e) => {
    dispatch(login());
    dispatch(someFn({ data: "data" })); // payload 전송
  };
  return <form onSubmit={(e) => submitHandler(e)}>{/* ... */}</form>;
};

export default Auth;
```
