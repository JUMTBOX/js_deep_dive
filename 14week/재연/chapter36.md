# 36 디스트럭처링 할당

- 구조 분해 할당은 구조화된 배열과 같은 이터러블 객체 또는 객체를 destructuring 하여 1개 이상의 변수에 개별적으로 할당하는 것을 말한다. 배열과 같은 이터러블 또는 객체 리터럴에서 필요한 값만 추출하여 변수에 할당할 때 유용하다.

### 36.1 배열 디스트럭처링 할당

- ES5에서 구조화된 배열을 디스트럭처링하여 1개 이상의 변수에 할당하는 방법은 다음과 같다.

```jsx
var arr = [1, 2, 3];

var one = arr[0];
var two = arr[1];
var three = arr[2];

console.log(one, two, three); //  1 2 3
```

- ES6의 배열 디스트럭처링 할당은 배열의 각 요소를 배열로부터 추출하여 1개 이상의 변수에 할당한다. 이때 <b>배열 디스트럭처링 할당의 대상(할당문의 우변)은 이터러블이어야 하며, 할당 기준은 배열의 인덱스다.</b>

```jsx
const arr = [1, 2, 3];
const [one, two, three] = arr;

console.log(one, two, three); //  1 2 3
```

- 배열 디스트럭처링 할당을 위해서는 할당 연산자(=) 왼쪽에 값을 할당받을 변수를 선엉해야 한다. 이때 뱐수를 배열 리터럴 형태로 선언한다.

```jsx
const [x, y] = [1, 2];
```

- 이때 우변에 이터러블을 할당하지 않으면 에러가 발생한다.

```jsx
const [x, y] // SyntaxError: Missing initializer in destructuring declaration;

const [a,b] = {}; // TypeError: {} is not iterable
```

- 배열 디스트럭처링 할당의 변수 선언문은 다음처럼 선언과 할당을 분리할 수도 있다. 단, 이 경우 const 키워드로 변수를 선언할 수 없으므로 권장하지 않는다.

```jsx
let x, y;
[x, y] = [1, 2];
```

- 배열 디스트럭처링 할당의 기준은 배열의 인덱스이다. 즉, 순서대로 할당된다. 이때 변수의 개수가 반드시 일치할 필요는 없다.

```jsx
const [c, d] = [1];
console.log(c, d); // 1 undefined

const [e, f] = [1, 2, 3];
console.log(e, f); // 1 2

const [g, , h] = [1, 2, 3];
console.log(g, h); // 1 3
```

- 배열 스트럭처링 할당을 위한 변수에 기본값을 설정할 수 있다.

```jsx
const [a, b, c = 3] = [1, 2];
console.log(a, b, c); // 1 2 3

const [e, f = 10, g = 3] = [1, 2];
console.log(e, f, g); // 1 2 3
```

- 배열 디스트럭처링 할당을 위한 변수에 Rest 파라미터와 유사하게 Rest 요소를 사용할 수 있다.

```jsx
const [x, ...y] = [1, 2, 3];
console.log(x, y); // 1 [2,3]
```

### 36.2 객체 디스트럭처링 할당

- ES5에서는 객체의 각 프로퍼티를 디스트럭처링하여 변수에 할당하기 위해서는 프로퍼티 키를 사용해야 한다.

- ES6의 객체 디스트럭처링 할당은 객체의 각 프로퍼티를 객체로부터 추출하여 1개 이상의 변수에 할당한다. 이때 객체 디스트럭처링 할당의 대상은 객체이어야 하며, <b>할당 기준은 프로퍼티 키다.</b> 즉, 순서는 의미가 없으며 선언된 변수 이름과 프로퍼티 키가 일치하면 할당된다.

```jsx
const user = { fN: "jae", ln: "yang" };
const { fn, ln } = user;
console.log(fn, ln); //jae yang
```

- 배열 디스트럭처링 할당과 마찬가지로 객체 디스트럭처링 할당을 위해서는 할당 연산자 왼쪽에 프로퍼티 값을 할당받을 변수를 선언해야 한다. 이때 변수를 객체 리터럴 형태로 선언한다.

- 이때 우변에 객체 또는 객체로 평가될 수 있는 표현식을 할당하지 않으면 에러가 발생한다.

- 객체의 프로퍼티 키와 다른 변수 이름으로 프로퍼티 값을 할당받으려면 다음과 같이 변수를 선언한다.

```jsx
const user = { firstName: "jae", lastName: "yang" };

const { lastName: ln, firstName: fn } = user;

console.log(fn, ln); // jae yang;
```

- 객체 디스트럭처링 할당을 위한 변수에 기본값을 설정할 수 있다.
- 객체 디스트럭처링 할당은 객체를 인수로 전달받는 함수의 매개변수에도 사용할 수 있다. [ex - React의 prop]

- 배열의 요소가 객체인 경우 배열 디스트럭처링 할당과 객체 디스트럭처링 할당을 혼용할 수 있다.

```jsx
const todos = [
  { id: 1, content: "HTML", completed: true },
  { id: 2, content: "CSS", completed: false },
  { id: 3, content: "JS", completed: false },
];

//todos 배열의 두 번째 요소인 객체로부터 id 프로퍼티만 추출한다.
const [, { id }] = todos;
console.log(id); // 2
```

- 중첩 객체의 경우 다음과 같이 사용한다.

```jsx
const user = {
  name: "Lee",
  address: {
    zipCode: "03068",
    city: "Seoul",
  },
};

const {
  address: { city },
} = user;
console.log(city);
```

- 객체 디스트럭처링 할당을 위한 변수에 Rest 파라미터나 Rest 요소와 비슷하게 Rest 프로퍼티를 사용할 수 있다.

```jsx
const { x, ...rest } = { x: 1, y: 2, z: 3 };
console.log(x, rest); // 1 {y:2, z:3};
```

# 면접 예상 질문

## 💥 ~~ 이란?

# 이야기하고 싶은 것

```jsx
const obj = { a: 1, b: 2, c: 3 };

for (const [key, val] of Object.entries(obj)) {
  console.log("키값", key);
  console.log("밸류값", val);
}

console.log(Object.entries(obj));
```
