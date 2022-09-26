# 의존적 state의 최신성 보장

## 1. 자기 의존적 state

직전의 state를 반영하여 state를 변화시킬 때 setState의 인자로 콜백을 사용하는것이 가장 안전한 방법이다. 최신을 보장함

```jsx
function App() {
  const [num, setNum] = useState(1);

  useEffect(() => {
    setNum(num + 1); // 스케쥴1: setNum(2)
    setNum(num + 1); // 스케쥴2: setNum(2)
  }, []); //  스케쥴 1,2 진행 후 App 1회 렌더링

  const handleClick = () => {
    console.log(num); // 출력: 2
  };
}
```

```jsx
function App() {
  const [num, setNum] = useState(1);

  useEffect(() => {
    setNum(num + 1);
    setNum((_num) => _num + 1); //prev 는 최신의 num을 보장
  }, []);

  const handleClick = () => {
    console.log(num); // 출력: 3
  };
}
```

## 2. 다른 state에 의존적인 state

다른 state에 의존해서 자신의 state가 변화하는 것은 최신의 state를 보장하지 못할 수 있음

```jsx
function App() {
  const [firstName, setFirstName] = useState("성호");
  const [lastName, setLastName] = useState("조");
  const [fullName, setFullName] = useState(firstName + " " + lastName); //다른 스테이트에 의존적

  const handleLastNameChange = () => {
    // click! => lastName은 "박"
    setLastName("박");
  };

  const handleConsole = () => {
    //click! => 출력: "성호 조", 최신보장 x
    console.log(fullName);
  };
}
```

<br>

## 2-1 useEffect의 의존성 배열 이용하여 최신화 보장

```jsx
function App() {
  const [firstName, setFirstName] = useState("성호");
  const [lastName, setLastName] = useState("조");
  const [fullName, setFullName] = useState(firstName + " " + lastName); //다른 스테이트에 의존적

  useEffect(() => {
    setFullName(firstName + " " + lastName);
  }, [lastName, firstName]); // 최신성 보장

  const handleLastNameChange = () => {
    // click! => lastName은 "박"
    setLastName("박");
  };

  const handleConsole = () => {
    //click! => 출력: "성호 박"
    console.log(fullName);
  };
}
```

## 2-2 일반 선언

직접 state를 변화시킬 일이 없다면 바닐라에서 선언하듯이 선언하고 사용할 수 있다.

```jsx
function App() {
  const [firstName, setFirstName] = useState("성호");
  const [lastName, setLastName] = useState("조");
  const realFullName = firstName + " " + lastName;

  const handleLastNameChange = () => {
    // click! => lastName은 "박"
    setLastName("박");
  };

  const handleConsole = () => {
    console.log(realFullName); //출력: "성호 박"
  };
}
```

<br>

## 2-2 상태들의 성격이 유사하다면 하나의 state로 객체화

<br>

```jsx
//객체화 전

const [emailIsValid, setEmailIsValid] = useState(null);
const [emailValue, setEmailValue] = useState("");

const handleInput = (e) => {
  setEmailValue(e.target.value);
};

const handleValidation = () => {
  setEmailIsValid(emailValue.includes("@"));
};

//위 처럼 사용해도 작동을 잘 하지만 잠재적인 위험성이 있는 코드
```

```jsx
//객체화 적용

const [emailState, setEmailState] = useState({ value: "", isValid: null });

const handleInput = (e) => {
  setEmailState({
    value: e.target.value,
    isValid: e.target.value.includes("@"),
  });
};

// 다른 state에 의존적이지 않은 하나의 state이다.
```

<br>

## 2-3 useReducer 이용

```js
const emailReducer = (state, action) => {
  if (action.type === "USER_INPUT") {
    return { value: action.val, isValid: action.val.includes("@") };
  }
  return { value: "", isValid: false };
};

const App = () => {
  const [emailState, dispatchEmail] = useReducer(emailReducer, {
    value: "",
    isValid: null,
  });

  const emailChangeHandler = (event) => {
    dispatchEmail({ type: "USER_INPUT", val: event.target.value });
  };
};
```

<br>

## 리덕스 이용(?)
