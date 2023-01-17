# Typescript 이론 정리

### Type 정의 방식

1. 명시적 정의(변수 선언 시 타입 정의)
   - let a: boolean = true
2. 타입 추론(변수만 생성)
   - let b = "hello"
   - b가 string 타입이라고 스스로 추론

- 명시적 정의보다 추론의 방법이 더 나음

### Types of TS

- 배열: 자료형[]
- 숫자: number
- 문자열: string
- 논리: boolean

### optional(물음표 사용)

```typescript
const player: {
  name: string;
  age?: number;
} = {
  name: "nico",
};
```

- if(player.age < 10)으로 작성 시 player.age가 undefined일 가능성이 있다고 알려줌
  - if(player.age && player.age < 10)이 올바른 코드

### Alias(별칭) 타입

```typescript
type Player = {
  name: string;
  age?: number;
}; // 대문자로 시작

const nico: Player = {
  name: "nico",
};

/* 함수에서 사용하는 방법 */

function playerMaker(name: string): Player {
  return {
    name,
    // name: name이 원칙이지만 같으면 생략 가능
  };
}

/* 화살표 함수에서 사용하는 방법 */

const playerMaker = (name: string): Player => ({ name });
```

- 객체 타입뿐만 아니라 모든 타입에 별칭 지정 가능함
- but, 과하게 재사용은 금지

### readonly 사용

```typescript
type Player = {
  readonly name: string;
  age?: number;
};
```

- 읽기 전용으로 지정되어 최초 선언 후 수정이 불가능함(불변성을 가지게 됨)

### Tuple

- 정해진 개수와 순서에 따라 배열 선언

```typescript
const player: [string, number, boolean] = ["nico", 1, true];

const player: readonly [string, number, boolean] = ["nico", 1, true];
// readonly와 병합해서 사용 가능
```

### any

- 무엇이든 입력할 수 있게 허용됨 (타입체크를 비활성화 시킨다는 의미)

## Typescript에만 있는 타입

### void

- 값을 반환하지 않는 함수의 반환 값을 나타냄
- return 문이 없거나 return 문에서 명시적 값을 반환하지 않을 때 유추되는 타입

```typescript
function hello() {
  console.log("x");
}
```

### unknown

- 모든 값을 나타냄
- 변수의 타입을 미리 알지 못 할 때 사용

```typescript
let a: unknown;

if (typeof a === "number") {
  let b = a + 1;
}

if (typeof a === "string") {
  let b = a.toUpperCase();
}
```

### never

- 함수가 절대 return하지 않을 때 발생
- 함수가 예외를 throw하거나 프로그램 실행을 종료함을 의미

```typescript
function hello(): never {
  throw new Error("zzz");
}
```

## Function

### Call Signatures

- 함수의 매개 변수와 반환 타입을 미리 선언

```typescript
type Add = (a: number, b: number) => number;

const add: Add = (a, b) => a + b;
```

### Overloading

- 직접 작성하기보다는 외부 라이브러리에 자주 보이는 형태
- 하나의 함수가 복수의 Call Signature를 가질 때 발생

```typescript
type Add = {
  (a: number, b: number): number;
  (a: number, b: string): number;
};

const add: Add = (a, b) => {
  if (typeof b === "string") return a;
  return a + b;
};
```

### Polymorphism

- 인자들과 반환 값에 대하여 형태(타입)에 따라 그에 상응하는 형태(타입)를 가질 수 있음

```typescript
type SuperPrint = {
  <T>(arr: T[]): void;
};
```

### Generics

- **제네릭은 선언 시점이 아니라 생성 시점에 타입을 명시하여 하나의 타입만이 아닌 다양한 타입을 사용할 수 있도록 하는 기법**
- 재사용 가능한 컴포넌트를 만들기 위해 사용하는 기법(위의 Polymorphism과 한 몸이라 생각)
- 제네릭을 처음 인식했을 때와 제네릭의 순서를 기반으로 제네릭 타입을 알게됨
- any와의 차이점 : 타입스크립트의 타입 체커로부터 보호를 받을 수 있음(any는 못받음)
  - 우리가 하는 요청에 따라 call signature를 생성함

```typescript
type SuperPrint = <T, M>(a: T[], b: M) => T;
```
