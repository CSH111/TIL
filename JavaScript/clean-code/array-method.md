# array 메소드 사용 형식

파라미터를 객체형태로 받으면 가독성이 좋아지는 경우가 많다.

```js
const arr = [
  [1, 2],
  [3, 4],
  [5, 6],
];

const newArr1 = arr.map((item) => item[1]); // 평소쓰던거

const newArr2 = arr.map(([a, b]) => b); //새로 알게된형식. 가독성 good

console.log(newArr); //출력: [2, 4, 6]
```

## 응용

함수만들때에도 유용

```js
function BadFn(arr) {
  const first = arr[0];
  const second = arr[1];
  // ....
}
// 가독성 별로

function goodFn([first, second]) {
  //...
}
//가독성 good
```
