# Date 표준내장객체

- Date 객체는 특성 시점의 시간과 그 시간을 다루 수 있는 다양한 메소드를 가지고있다.

## 기초

```js
//인자 없이 사용시 현재기기의 현재시간을 담은 인스턴스생성
const myTime = new Date();
/*
Tue Nov 08 2022 17:22:54 GMT+0900 (한국 표준시)
getDate()
...
... 메소드들
*/
```

```js
//인스턴스 생성 1
// 날짜 형식을 담은 string을 인자로 받음. 후에 형식 변환 메소드를 위해 유용하게 사용가능

new Date("2022-11-26T13:30:00"); // Tue Nov 08 2022 17:22:54 GMT+0900 (한국 표준시)
new Date("2022-11-26"); // 시간이 생략되면 자동으로 09:00:00으로 설정됨.
new Date("2022-11"); // 일이 생략되면 자동으로 1일로 설정됨.
new Date("2022"); // 월이 생략되면 자동으로 1월로 설정됨.
```

```js
//인스턴스 생성 2
// milliseconds 를 인자로 받음

//Date.now() 는 Date 의 static 메소드로 현재 시간을 밀리세컨드로 나타냄
const mili = Date.now(); // 1667897182224

new Date(mili); // Tue Nov 08 2022 17:46:22 GMT+0900 (한국 표준시)
```

```js
//인스턴스 생성3
// new Date(년, 월[, 일, 시, 분, 초, 밀리초])
//일 생략 - 1일, 시생략 0시
// 월은 0부터 1월..
new Date(2022, 0, 15); // Sat Jan 15 2022 00:00:00 GMT+0900 (한국 표준시)
```

<br>

## 활용 - 형식변환

- api 등에서 받아온 다양한 형식의 날짜 데이터를 내장 date 메소드를 이용해 가공할 수 있다.

```js
const dateFromApi = "2022-11-08T08:57:16.975Z"; // ISO 형식

const originDateObj = new Date(dateFromApi); // date객체로 만들어서 메소드활용

originDateObj.toLocaleString("kr-KR"); // '2022. 11. 8. 오후 5:56:46'
originDateObj.toLocaleString(""); //생략시 기기의 국가 설정. '2022. 11. 8. 오후 5:56:46'

// options 참고 - mdn

const optionsA = {
  month: "long", // 영어에서만 long, short, 의미(mar, march)
  day: "numeric",
  weekday: "long",
};

const optionsB = {
  month: "long",
  day: "2-digit",
  weekday: "shor",
};

const optionsC = {
  year: "numeric",
  month: "long",
  day: "2-digit",
};

const optionsD = {
  year: "2-digit",
  month: "long",
};

originDateObj.toLocaleString("kr-KR", optionsA); // 1월 1일 토요일
originDateObj.toLocaleString("kr-KR", optionsB); // 11월 08일 (화)
originDateObj.toLocaleString("kr-KR", optionsC); // 2022년 11월 08일
originDateObj.toLocaleString("kr-KR", optionsD); // 22년 11월
```

<br>

## ref

- tolocaleSting options MDN  
  https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/DateTimeFormat/DateTimeFormat#options
