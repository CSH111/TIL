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

## createAsyncThunk

... 작성중 ...
