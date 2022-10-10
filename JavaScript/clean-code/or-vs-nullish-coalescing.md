# ?? vs ||

nullish coalescing operator ?? 는 OR operator || 대신 유용하게 쓸 수 있다.

|| 는 falsy 한 값에 따라 반응하지만

?? 은 null 또는 undefined에만 반응한다.

|| 을 사용할 경우에 의도된 number 0 등에 예기치 못한 결과를 가져올 수 있다. 그럴때 ?? 를 사용하면 바람직

```js
console.log(0 || "not found"); // "not found"
console.log(0 ?? "not found"); // 0

console.log("" || "not found"); // "not found"
console.log("" ?? "not found"); // ""

console.log(false || "not found"); // "not found"
console.log(false || "not found"); // false
```

### 참조

https://stackoverflow.com/questions/61480993/when-should-i-use-nullish-coalescing-vs-logical-or
