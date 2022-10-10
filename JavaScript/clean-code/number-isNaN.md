# isNaN() vs Number.isNaN()

isNaN(value) 는 값이 Number 타입인지 아닌지 판별한다.

Number.isNaN(value) 는 값이 NaN 타입인지 아닌지 판별한다.

```js
isNaN("i'm string"); // true

Number.isNaN("i'm string"); //false
```

isNaN 은 값을 숫자로 형변환한 것과 마찬가지로 작동  
(= isNaN(value) 는 Number.isNaN(Number(value)) 과 동일하게 작동 )

Number.isNaN 은 의도하지 않은 형 변환을 방지하기 위해 ES6 추가된 것

가능하다면 Number.isNaN 을 사용하는게 바람직
