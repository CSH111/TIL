# 삼항연산자와 그 대안

jsx 에서는 if 문, for문 등 사용못함 => 삼항연산자 사용

삼항연산자 형식

```jsx
function Expenses(props) {
  return (
    <Card className="expenses">
      <ExpenseFilter />
      {filteredItems.length === 0 ? (
        <p>no data</p>
      ) : (
        filteredItems.map((item) => (
          <ExpenseItem
            title={item.title}
            date={item.date}
            amount={item.amount}
            key={item.id}
          />
        ))
      )}
    </Card>
  );
}
```

가독성이 나쁠 때가 있다. 그 때의 대안 &&와 변수이용

<br>

## &&연산자 이용하기

```jsx
function Expenses(props) {
  return (
    <Card className="expenses">
      <ExpenseFilter />
      {filteredItems.length === 0 && <p>no data</p>}
      {filteredItems.length > 0 &&
        filteredItems.map((item) => (
          <ExpenseItem
            title={item.title}
            date={item.date}
            amount={item.amount}
            key={item.id}
          />
        ))}
    </Card>
  );
}
```

읽기 편한 코드가 되었다. 그렇지만 여전히 한눈에 요소들을 파악하기는 어렵다.

<br>

## 변수이용

```jsx
function Expenses(props) {
  let expenseContents = <p>no data</p>; //let 사용
  if (filteredItems.length > 0) {
    expenseContents = filteredItems.map((item) => (
      <ExpenseItem
        title={item.title}
        date={item.date}
        amount={item.amount}
        key={item.id}
      />
    ));
  }

  return (
    <Card className="expenses">
      <ExpenseFilter />
      {expenseContents}
    </Card>
  );
}
```

이제 한눈에 구조파악 가능..

cf. 실제로 변동되는 변수값은 보통 useState를 이용하지만,
변수값에 변동에 필요한 state가 들어가 있다면 `let 변수명` 등으로 편하게 사용할 수 있다.
