# 리덕스의 비동기처리

기본적으로 컴포넌트 내부에서 비동기 로직을 처리한 뒤 리덕스 스토어로 값을 보낼 수 있다. but lean 컴포넌트 등의 이유로 로직을 리덕스에 담아두고 싶다면 다른 방법이 필요

<br>
 
## thunk 사용하기

`createSlice`를 사용해 reducers 를 정의 할때 자동적으로 actions 객체를 만들어 준다. 여기서는 비동기처리를 할 수 없다.(redux내부 로직이 이유)

```jsx
// src/store/auth.js

const authSlice = createSlice({
  name: "auth",
  initialState: initailAuthState,
  reducers: {
    login(state) {
      state.isAuthenticated = true;
    },
    ...
  }
  // authSlice.acions가 자동으로 생성 된다.
```

자동으로 생성되는 actions 말고 action 직접 생성할 수 있다.
그렇게 되면 해당 action을 정의 할 때 비동기 처리 가능함

<br>

```jsx
// store/cart-actions.js

import { cartAcions } from "./cart-slice";
import { uiActions } from "./ui-slice";

// 비동기 함수를 반환해준다.
export const getCartData = () => {
  const { showNotification } = uiActions; // 에러처리 액션
  const { setItems } = cartAcions; // 데이터 출력 액션

  // 첫번째 인자로 dispatch가 들어오게되어(내부로직) action을 가져와서 dispatch할 사용할 수있다.
  return async (dispatch) => {
    try {
      const res = await axios.get("/data");
      dispatch(setItems(res.data));
    } catch (err) {
      dispatch(
        showNotification({
          status: "error",
          title: "error!",
          message: "error getting cart data",
        })
      );
    }
  };
};
```

커스텀 액션 사용 in App.js

```jsx
// App.js
import { getCartData } from "./ui-actions";

function App() {
  const dispatch = useDispatch();

  useEffect(() => {
    dispatch(getCartData()); //커스텀 액션을 디스패치
  }, []);

  return <>...</>;
}
```

반복적으로 처리되는 데이터 처리 로직(pending, fulfilled, rejected 등)을 간편하게 하는 등 `thunk`를 편하게 쓰기 위해 툴킷에서는 `createAsyncThunk`라는 api를 지원해준다.

<br>

## createAsyncThunk 이용하기

위 처럼 직접 생성한 액션에서 로직에 따라 직접 dispatch 하는 것은 경우에 따라 바람직하지 않을 수 있음.

`createAsyncThunk`를 이용해 데이터를 fetch해오는등 최소한의 비동기 작업만들 분리해놓고 그에따른 후속작업은 개별 슬라이스 `extraReducer`에 쉽게 작성해 놓을 수 있음.

```jsx
// store/cart-actions.js

import { createAsyncThunk } from "@reduxjs/toolkit";

const getCartData = createAsyncThunk("GET_CART_DATA", async () => {
  const res = await axios.get("/cart.json");
  return res.data; //리턴값은 바로 payLoad에 담김

  // 핵심로직 및 에러 처리시 개별 담당 슬라이스에 디스패치하는것이아니라
  // 개별 슬라이스 내부에서 미리 정의가능
});
// ...

export { getCartData };
```

```jsx
// store/cartSlice.js, 핵심로직처리(get 후 items에 넣기)

import { getCartData } from "./cart-actions";

const initialState = {
  items: [], //...
};
const cartSlice = createSlice({
  name: "cart",
  initialState,
  reducers: {
    //...
  },
  //비동기 액션에 대해 pending, fulfilled, rejected 상태에 대한 후속 작업을 정의할 수 있다.
  extraReducers: (builder) => {
    builder.addCase(getCartData.fulfilled, (state, action) => {
      //createThunk 내부의 함수 리턴값은 actions.payload에 담김
      state.items = action.payload.items;
      //...
    });
  },
});
//...
```

```jsx
// store/uiSlice.js   , getCartData의 송신상태표시 로직(ui)

import { getCartData } from "./cart-actions";

const uiSlice = createSlice({
  name: "ui",
  initialState: { notification: null },
  reducers: {
    // ...
  },
  extraReducers: (builder) => {
    builder.addCase(getCartData.pending, (state, action) => {
      state.notification = {
        status: "pending",
        title: "pending...",
        message: "pending sending cart data...",
      };
    });
    builder.addCase(getCartData.fulfilled, (state, action) => {
      state.notification = {
        status: "success",
        title: "success!",
        message: "success sending cart data!",
      };
    });
    builder.addCase(getCartData.rejected, (state, action) => {
      state.notification = {
        status: "error",
        title: "error!",
        message: "error sending cart data",
      };
    });
  },
});
```

```jsx
// App.js
import { getCartData } from "./ui-actions";

function App() {
  const dispatch = useDispatch();

  useEffect(() => {
    dispatch(getCartData());
    // extra리듀서 정의시 콜백인자의 action.payload에 해당 액션의 리턴값이 들어간다.
    // 만약 여기서  argument를 넣는다면 action.args에 들어가게 된다.
    //일반 커스텀 액션 및 리듀서의 자동 생성 액션과는 다른 createThunk의 특징이라면 특징..
  }, []);

  return <>...</>;
}
```
