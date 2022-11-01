# intersection-observer API

- `intersection-observer API`는 브라우저에 특정 노드가 직접 출력 되었을 때 후속 작업을 설정할 수 있도록 도와주는 api 이다.
- 사용자의 `scroll`에 따라 특정 작동을 하게끔 구현할 때 매우 유용..
- `scroll event`가 너무 무겁게 작동할 때 대안으로 유용할듯하다.

```html
<!-- index.html -->
<!-- ... -->
<body>
  <div class="box">하이</div>
  <div class="box">하이</div>
  <div class="box">하이</div>
  <div class="box">하이</div>
  <div class="box six">하이</div>
  <div class="box">하이</div>
  <div class="box">하이</div>
  <div class="box">하이</div>
  <div class="box">하이</div>
  <script src="src/index.js"></script>
</body>
<!-- ... -->
```

```js
const observer = new IntersectionObserver((entries) => {
  // entries 는 observe 중인 모든 element임

  // 수행하고싶은 작업: 노드를 만날 때마다 콘솔출력
  entries.forEach((entry) => {
    console.log(entry);
  });
});

const box6 = document.querySelector(".six");

observer.observe(box6); // observer가 box6를 observe 실행

// observe 중인 box6가 브라우저출력 화면에 나오기 시작할때, 완전히 사라졌을 때 observer의 콜백을 실핸한다.
```

```js
// entry객체의 내부

time: 1221459.7999999523
rootBounds: null
boundingClientRect: DOMRectReadOnly
intersectionRect: DOMRectReadOnly
isIntersecting: true    // true이면 화면에 출력중임을뜻함
isVisible: false
intersectionRatio: 0.017550284042954445 // 0이상이면 출력중임을 뜻함
target:
<div class="box six">하이</div>
<constructor>: "IntersectionObserverEntry"
```

<br>

## 응용

- 무한스크롤
  - 페이지 맨 하단에 보이지 않는 엘리먼트를 만들어두고 observe한다면 스크롤이 끝났을 때 새로 데이터를 받아오는 식으로 구현 가능
