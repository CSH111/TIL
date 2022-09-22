# 컴포넌트에서 ref 사용하기1 - forwardRef

커스텀 컴포넌트에서 ref를 사용하기 위해서는 `forwardRef` 를 이용해야한다.

```js
//App.js

const App = (props, ref) => {
  const myInput = useRef()

  const handleClick = () => {
    myInput.current.focus()
  }

  return (
    <Header />
    <FancyInput
      ref={myInput}         //FancyInput.js 에서 별도의 처리필요
      type={props.type}
      onChange={props.onChange}
    ></FancyInput>
    <Button onClick={handleClick}/>
  );
};


//FancyInput.js

//React.forwardRef 이용해야함.(형식)

const FancyInput = React.forwardRef((props, ref) => {
  return (
    <input
      ref={ref}
      type={props.type}
      id={props.id}
    />
  );
});

```

<br>

## useImperativeHandle 훅을 이용한 method 생성

```js
//FancyInput.js


const FancyInput = React.forwardRef((props, ref) => {
 useImperativeHandle(ref, () => ({    //메소드 생성
    focusAndAlert: () => {
      ref.current.focus();
      alert('focused!!')
    }
  }));

  return (
    <input
      ref={ref}
      type={props.type}
      id={props.id}
    />
  );
});

//App.js

const App = (props, ref) => {
  const myInput = useRef()

  const handleClick = () => {
    myInput.current.focusAndAlert()   //생성한 메소드사용
  }

  return (
    <Header />
    <FancyInput
      ref={myInput}
      type={props.type}
      onChange={props.onChange}
    ></FancyInput>
    <Button onClick={handleClick}/>
  );
};

```
