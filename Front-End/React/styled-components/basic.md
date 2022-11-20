# 스타일드 컴포넌트 기본

## 스타일드 컴포넌트는 어떻게 스타일을 입히는 것일까?

```jsx
const StyledP = styled.p`
  width: 100px;
  height: 100px;
  background-color: beige;
`;

const App = () => {
  <StyledP>안녕하세요</StyledP>;
};
```

- `styled`라는 객체(함수)를 이용해 p태그에 특정한 클래스를 주고 해당 클래스만들 위한 css를 생성한다.

<img src="../../../img/styled-components/styleClass.JPG" />

<br>

## 커스텀 컴포넌트에 스타일드 컴포넌트 입히기

```jsx
const StyledMyComponent = styled(MyComponent)`
  width: 100px;
  height: 100px;
  background-color: azure;
`;

const MyComponent = () => {
  return <main>하이</main>;
};

const App = () => {
  <MyComponent>안녕하세요</MyComponent>;
};
```

- 이렇게 되면 스타일이 반영되지않는다 왜일까?
- `styled`함수를 통해 `MyComponent`에게 스타일 적용을 위한 클래스를 넘겨주지만 정작 최종으로 출력되는 `main`태그 에서는 아무런 클래스를 전달 받지 못한다.

```jsx
const MyComponent = ({ className }) => {
  return <main className={className}>하이</main>;
};
```

- 위와 같이 styled 함수에서 생성된 클래스를 최종 출력되는 컴포넌트로 넘겨주어야 정상적으로 스타일이 적용된다.

<br>

## css 구문에서 컴포넌트 직접 부르기

- 스타일드 컴포넌트에서는 기본적으로 sass 문법을 지원한다.

```jsx
const Container = styled.div`
  height: 100vh;
  background-color: beige;

  /* sass의 중첩 구문을 이용해 스타일링 가능 */
  p {
    color: purple;
  }
`;
const App = () => {
  return (
    <Container>
      <p>안녕하세요</p>
    </Container>
  );
};
```

- 여태 사용하면서 몰랐던것은 중첩 태그에 태그대신 컴포넌트 자체를 넣을 수 있다는점...

```jsx
const StyledP = styled.p``;
const Container = styled.div`
  ${StyledP} {
    background-color: purple;
  }
`;
// 스타일이 잘 적용된다.
const App = () => {
  return (
    <Container>
      <StyledP>안녕하세요</StyledP>
    </Container>
  );
};
```

- 스타일드 컴포넌트로 생성지않은 커스텀 컴포넌트는 적용되지 않는다. 아마 css상 네스팅된 컴포넌트를 구분하기 위해 styled에서 부여한 class 를 이용하는것으로 보인다(추후확인하기)
