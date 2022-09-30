# reusable 폼 제작기(context 이용)

## index

1.  [제작배경](#제작배경)
2.  [사용법](#사용예)
3.  [내부로직](#내부로직)
4.  [referance](#referance)

<br>
<br>

## 제작배경

value 컨트롤이 너무 귀찮아서 form 을 재사용 가능하도록 편하게 이용하고 싶다는 생각에 서칭해 보았다.

웹상에서 쉽게 찾을 수 있는 reusable form 코드들이 많이 있었지만 나에겐 복잡하고 번거롭게 느껴서 불만족스러웠다.

해당 코드들 중 대부분에서 useReducer를 이용하거나 별도의 배열에 input의 속성을 넣는 식으로 폼을 생성했는데 그게 나에겐 복잡하고 불편하게 느껴졌다.

별도의 객체 및 배열 작성없이 인라인으로 prop을 넘겨주는 식으로 사용할 수 있는 reusable form을 만들고자 했다.

<br>

## 사용법

```jsx
// LogiinForm.js

import { Form } from "./ReusableForm/Form";
import Input from "./ReusableForm/Input";
import { useRef } from "react";

const LoginForm = () => {
  const emailInput = useRef();
  const handleSubmit = (context) => {
    // submit 후 밸류 처리 방법

    //  - context를 간접적으로 조작
    //  - context가 위치한 개별 Form으로 context 처리함수 전송

    // context.values 로 input value 이용
    //ex) axios.post("/api/...", context.values)
    console.log(context.values);
    emailInput.current.focus(); // ref 이용

    // 모든 인풋 value 비우기 1
    context.setValues({});

    // 모든 인풋 value 비우기 2 - email, pw 는 Input의 name prop
    context.setValues({ email: "", pw: "" });

    //pw 만 비우기
    context.setValues((values) => ({ ...values, pw: "" }));
  };

  // Input의 label prop으로 라벨 생성X
  // name prop필수
  // value 컨트롤은 자동화 되어있음
  return (
    <Form onSubmit={handleSubmit}>
      <Input
        label="이메일"
        id="email"
        name="email"
        type="text"
        ref={emailInput}
      />
      <Input
        label="비밀번호" //
        id="pw"
        name="pw"
        type="password"
      />
      <button type="submit">제출</button>
    </Form>
  );
};

export default LoginForm;
```

- `handleSubmit`의 첫 번째 인자로 context를 컨트롤 할 수 있다.
- 스타일드 컴포넌트 이용가능

<br>

## 내부로직

```jsx
// ReusableForm/Form.js

// Form 컴포넌트 마다 컨텍스트 생성 및 Input과 공유

import { useState, useContext } from "react";

const FormContext = React.createContext(null);

const Form = ({ children, onSubmit }) => {
  const [values, setValues] = useState({});

  return (
    <FormContext.Provider value={{ values, setValues }}>
      <ValueSender onSubmit={onSubmit}>{children}</ValueSender>
    </FormContext.Provider>
  );
};

const ValueSender = ({ onSubmit, children }) => {
  const formCtx = useContext(FormContext);

  const handleSubmit = (e) => {
    e.preventDefault();
    onSubmit(formCtx); // onSubmit 처리 인자로 context 넘겨줌
  };

  return <form onSubmit={handleSubmit}>{children}</form>;
};

export { Form, FormContext };
// ValueSender 라는 이름에 대해 고민필요...
```

<br>

```jsx
// ReusableForm/Input.js
import React from "react";
import { useContext, useEffect } from "react";
import { FormContext } from "./Form";

// context로 value 컨트롤

const Input = React.forwardRef((props, ref) => {
  const formCtx = useContext(FormContext);
  const valueInContext = formCtx.values[props.name] ?? "";

  //name prop에 따라 context에 키와 초기값 부여
  useEffect(() => {
    formCtx.setValues((values) => ({ ...values, [props.name]: "" }));
  }, []);

  //value control
  const handleChange = (e) => {
    formCtx.setValues((values) => ({
      ...values,
      [props.name]: e.target.value,
    }));
    // 디바운스 적용하게끔 수정 가능
  };

  //label prop으로 라벨 생성, valueInContext가 밸류로 들어가 컨트롤가능
  return (
    <div className="control">
      <label htmlFor={props.id}>{props.label}</label>
      <input
        id={props.id}
        name={props.name}
        className={props.className}
        type={props.type}
        onChange={handleChange}
        value={valueInContext}
        ref={ref}
      />
    </div>
  );
});

export default Input;
```

제작 소요기간: 2일

<br>

## referance

How to Create a Reusable React Form component - Gerald Ezenagu

https://www.section.io/engineering-education/how-to-create-a-reusable-react-form/

<br>

React + Styled-Components | Reusable FORM Component - CodeFocus

https://www.youtube.com/watch?v=UGU0PZduIFg&t=671s&ab_channel=CodeFocus

<br>

contextAPI + styled-components 로 재사용 컴포넌트 만들기 - 개발화라리 Hwarang

https://www.youtube.com/watch?v=5RhCxzmp2yw&t=253s&ab_channel=%EA%B0%9C%EB%B0%9C%ED%99%94%EB%9D%BC%EB%A6%ACHwarang
