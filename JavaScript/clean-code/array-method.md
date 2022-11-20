# array 메소드 사용 형식

## 1. 파라미터 Destructuring assignment

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

### 응용

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

<br>

## 2. 배열의 마지막 인자 Destructuring assignment

```js
const arr = ["a", "b", "c", "d", "e", "f"];

// 일반적인 구조분해할당
const [a, b] = arr; // a = "a", b = "b"

// 배열의 마지막 부근 인자를 받고싶을 때 구조분해 할당
//slice 활용
const [e, f] = arr.slice(-2); // e = "e", f = "f"
```

<br>

## 3. 중복 없애기 Set 자료형 활용

```js
// Set 자료형은 중복을 허용하지 않는다는것 이용

const arr = [1, 2, 1, 2, 3];
const setArr = new Set(arr);
const newArr = [...setArr]; // [1, 2, 3]
```

<br>

## 4. split 이용 일치 갯수 세기

```js
// 문자열중 a 의 갯수는?

const str = "asdfa";
str.split("a").length - 1;
```
