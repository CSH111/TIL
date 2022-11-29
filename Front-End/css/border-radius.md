# border-radius

## 유용한 트릭

### pill(알약)모양

```css
.box1 {
  background-color: coral;
  width: 300px;
  height: 100px;
  border-radius: 9999px; /**/
}
```

- border-radius의 최대 설정값은 가로, 세로중 짧은 쪽의 50% 이다.
- 이것을 이용해 매우큰 값을 설정해 알약모양으로 사용

<br>

### 반응형 카드

```css
.box2 {
  background-color: coral;
  --width: 400px;
  --height: 200px;
  width: var(--width);
  height: var(--height);
  border-radius: calc(((var(--width) + var(--height)) / 2) * 0.05);
}
```

- width와 height의 길이에 비례해 둥근 모서리의 면적이 조정 되게끔 할 수있다.

<br>

## 헷갈릴 수 있는 개념들

```css
/*네 모서리 각각 설정*/
border-radius: 10px 20px 30px 50px;

/*대각선 끼리 설정( 나뭇잎 모양)*/
border-radius: 10px 30px;

/* 가로방향 반지름과 세로방향 반지름을 다르게 설정*/
border-radius: 10px/30px;
```

## 참고

https://stackoverflow.com/questions/29966499/border-radius-in-percentage-and-pixels-px-or-em
