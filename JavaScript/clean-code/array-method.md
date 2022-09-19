# array 메소드 사용 형식

```js
const arr = [
  [1, 2],
  [3, 4],
  [5, 6],
];

//const newArr = arr.map((item) => item[1]) 평소쓰던거

const newArr = arr.map(([a, b]) => b); //새로 알게된형식. 가독성 훨씬 졸음

console.log(newArr); //출력: [2, 4, 6]
```
