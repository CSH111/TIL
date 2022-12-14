# 이벤트 핸들러 네이밍

<br>

## 컨벤션1 - handleClick (~handler)

<br>

```jsx
function BoxArea() {
  const handleClick = () => {
    // .....창 닫는 로직...
    // .....창 닫는 로직...
  };
  return <div onClick={handleClick}></div>;
}
```

`onClick` 은 이벤트의 실행 트리거(실행 시점)을 의미한다. `on + 트리거`  
`handleClick` 은 이벤트 이후 작동할 함수의 이름이다.  
이것과 거의 비슷하게 `clickHandler` 라는 이름을 사용하기도 한다.
<br>

- 장점

  - 이벤트를 다루고 있는 함수 라는것이 눈에 잘 띈다.  
    <br>
    <br>

- 단점
  - `handleClick` 이라는 함수 명으로 해당 이벤트가 비즈니스 로직에서 어떤 일을 수행 할지 예측할 수없다.

<br>
<br>

## 컨벤션2 - no handle

<br>

```jsx
function BoxArea() {
  const closeBox = () => {
    // .....창 닫는 로직...
    // .....창 닫는 로직...
  };
  return <div onClick={closeBox}></div>;
}
```

`handleClick` 대신 일반적인 함수 이름을 사용한다.

<br>

- 장점

  - 함수 내부를 살펴보지 않아도 이벤트의 역할을 쉽게 알 수 있다.
    <br>
    <br>

- 단점
  - 함수만 봤을때 이벤트에 사용되고 있음을 알 수 없다.

<br>
<br>

## 컨벤션3 - handleAction

<br>

```jsx
function BoxArea() {
  const handleCloseBox = () => {
    // .....창 닫는 로직...
    // .....창 닫는 로직...
  };
  return <div onClick={handleBoxClose}></div>;
}
```

`handle + action(명사+동사 or 명사형)` .

  <br>

- 장점

  - 함수 내부를 살펴보지 않아도 이벤트의 역할을 쉽게 알 수 있다.
  - 이벤트를 다루고 있음을 표시할 수 있다.
    <br>
    <br>

- 단점
  - 함수만 봤을 때 어떤 이벤트종류(click인지 mouseEnter인지)에 의해 실행되는지 알 수 없다.

<br>
<br>

개인적으로 컨벤션3이 가장 마음에 든다.

`handleClick` 이 가장 익숙하지만 종종 가독성이 떨어지는 상황이 생기기도 했는데 그걸 어느정도 해결해주는 방식인듯 하다.
<br>
<br>

## Reference

https://jaketrent.com/post/naming-event-handlers-react  
https://blog.shiren.dev/2020-07-27-1/
