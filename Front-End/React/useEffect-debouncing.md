# useEffect 를 이용한 디바운싱

```jsx
useEffect(() => {
  const identifier = setTimeout(() => {
    setIsValid(email.includes("@") && pw.trim().length > 6);
  }, 500);

  return () => clearTimeout(identifier);
}, [email, pw]);

// 참고: email과 pw는 매 타이핑마다 변환되는 stated임
```

로그인 폼의 유효성 검사에서 활용한 예시이다.
