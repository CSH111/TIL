# 틸트연산자

- ~num 은 -(num + 1)을 리턴한다.
- ~~num 은 parseInt와 동일
- 자세한 내용은다음기회에..

<br>

## 틸트연산자의 활용

```jsx
// with indexOf
const str = "안녕 나는 성호";

console.log(~str.indexOf("나는") ? true : false); // true
console.log(~str.indexOf("지연") ? true : false); // false

// parseInt
const num = 1.45;
const nagative = -1.45;
console.log(~~num); // 1
console.log(parseInt(num)); // 1
console.log(~~nagative); // -1
console.log(parseInt(nagative)); // -1
```

- `string`, `array에서` 값의 존재 여부를 찾을 때 유용하게 활용가능
- `indexOf()`는 존재하지 않는 값은 -1 을 리턴
- 여기에 tilt 연산자를 사용하면 falsy값인 0으로 만들 수있다.

<br>

## vs includes(), parseInt

- find includes 등 메소드에 비해 브라우저 지원 범위가 넓음
- parseInt 보다 짧게쓰기 가능..
