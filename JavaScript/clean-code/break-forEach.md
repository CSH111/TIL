# forEach 메소드를 break 시키기

성능최적화를 위해 forEach를 돌다 break 시키고 싶을 때가 있다.
but forEach를 break 하는 것은 지원되지 않는다. 사용시 에러뜸

## 방법1 try catch 문

```js
const arr = ["a", "b", "c", "d"];

// c 에서 멈추고 싶은 상황
try {
  arr.forEach((elem) => {
    console.log(elem);
    if (elem === "c") throw Error;
  });
} catch {}

//출력
// a
// b
// c
```

<br>

## 방법2 for of 문

```js
const arr = ["a", "b", "c", "d"];

// c 에서 멈추고 싶은 상황

for (let elem of arr) {
  console.log(elem);
  if (elem === "c") break;
}

//출력
// a
// b
// c
```

catch 해서 처리할게 없다면 for of 쓰는게 좋을듯하다.

<br>

## 번외 for of 문에서 index를 사용하는 법(entries 활용)

```js
const arr = ["a", "b", "c", "d"];

// c 에서 멈추고 싶은 상황

for (let [idx, elem] of arr.entries()) {
  console.log(idx, elem);
  if (elem === "c") break;
}

//출력
// 0 a
// 1 b
// 2 c
```
