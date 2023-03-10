# πTypescript μ΄λ‘  μ λ¦¬

### Type μ μ λ°©μ

1. λͺμμ  μ μ(λ³μ μ μΈ μ νμ μ μ)
   - let a: boolean = true
2. νμ μΆλ‘ (λ³μλ§ μμ±)
   - let b = "hello"
   - bκ° string νμμ΄λΌκ³  μ€μ€λ‘ μΆλ‘ 

- λͺμμ  μ μλ³΄λ€ μΆλ‘ μ λ°©λ²μ΄ λ λμ

### Types of TS

- λ°°μ΄: μλ£ν[]
- μ«μ: number
- λ¬Έμμ΄: string
- λΌλ¦¬: boolean

### optional(λ¬Όμν μ¬μ©)

```typescript
const player: {
  name: string;
  age?: number;
} = {
  name: "nico",
};
```

- if(player.age < 10)μΌλ‘ μμ± μ player.ageκ° undefinedμΌ κ°λ₯μ±μ΄ μλ€κ³  μλ €μ€
  - if(player.age && player.age < 10)μ΄ μ¬λ°λ₯Έ μ½λ

### Alias(λ³μΉ­) νμ

```typescript
type Player = {
  name: string;
  age?: number;
}; // λλ¬Έμλ‘ μμ

const nico: Player = {
  name: "nico",
};

/* ν¨μμμ μ¬μ©νλ λ°©λ² */

function playerMaker(name: string): Player {
  return {
    name,
    // name: nameμ΄ μμΉμ΄μ§λ§ κ°μΌλ©΄ μλ΅ κ°λ₯
  };
}

/* νμ΄ν ν¨μμμ μ¬μ©νλ λ°©λ² */

const playerMaker = (name: string): Player => ({ name });
```

- κ°μ²΄ νμλΏλ§ μλλΌ λͺ¨λ  νμμ λ³μΉ­ μ§μ  κ°λ₯ν¨
- but, κ³Όνκ² μ¬μ¬μ©μ κΈμ§

### readonly μ¬μ©

```typescript
type Player = {
  readonly name: string;
  age?: number;
};
```

- μ½κΈ° μ μ©μΌλ‘ μ§μ λμ΄ μ΅μ΄ μ μΈ ν μμ μ΄ λΆκ°λ₯ν¨(λΆλ³μ±μ κ°μ§κ² λ¨)

### Tuple

- μ ν΄μ§ κ°μμ μμμ λ°λΌ λ°°μ΄ μ μΈ

```typescript
const player: [string, number, boolean] = ["nico", 1, true];

const player: readonly [string, number, boolean] = ["nico", 1, true];
// readonlyμ λ³ν©ν΄μ μ¬μ© κ°λ₯
```

### any

- λ¬΄μμ΄λ  μλ ₯ν  μ μκ² νμ©λ¨ (νμμ²΄ν¬λ₯Ό λΉνμ±ν μν¨λ€λ μλ―Έ)

## Typescriptμλ§ μλ νμ

### void

- κ°μ λ°ννμ§ μλ ν¨μμ λ°ν κ°μ λνλ
- return λ¬Έμ΄ μκ±°λ return λ¬Έμμ λͺμμ  κ°μ λ°ννμ§ μμ λ μ μΆλλ νμ

```typescript
function hello() {
  console.log("x");
}
```

### unknown

- λͺ¨λ  κ°μ λνλ
- λ³μμ νμμ λ―Έλ¦¬ μμ§ λͺ» ν  λ μ¬μ©

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

- ν¨μκ° μ λ returnνμ§ μμ λ λ°μ
- ν¨μκ° μμΈλ₯Ό throwνκ±°λ νλ‘κ·Έλ¨ μ€νμ μ’λ£ν¨μ μλ―Έ

```typescript
function hello(): never {
  throw new Error("zzz");
}
```

## Function

### Call Signatures

- ν¨μμ λ§€κ° λ³μμ λ°ν νμμ λ―Έλ¦¬ μ μΈ

```typescript
type Add = (a: number, b: number) => number;

const add: Add = (a, b) => a + b;
```

### Overloading

- μ§μ  μμ±νκΈ°λ³΄λ€λ μΈλΆ λΌμ΄λΈλ¬λ¦¬μ μμ£Ό λ³΄μ΄λ νν
- νλμ ν¨μκ° λ³΅μμ Call Signatureλ₯Ό κ°μ§ λ λ°μ

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

- μΈμλ€κ³Ό λ°ν κ°μ λνμ¬ νν(νμ)μ λ°λΌ κ·Έμ μμνλ νν(νμ)λ₯Ό κ°μ§ μ μμ

```typescript
type SuperPrint = {
  <T>(arr: T[]): void;
};
```

### Generics

- **μ λ€λ¦­μ μ μΈ μμ μ΄ μλλΌ μμ± μμ μ νμμ λͺμνμ¬ νλμ νμλ§μ΄ μλ λ€μν νμμ μ¬μ©ν  μ μλλ‘ νλ κΈ°λ²**
- μ¬μ¬μ© κ°λ₯ν μ»΄ν¬λνΈλ₯Ό λ§λ€κΈ° μν΄ μ¬μ©νλ κΈ°λ²(μμ Polymorphismκ³Ό ν λͺΈμ΄λΌ μκ°)
- μ λ€λ¦­μ μ²μ μΈμνμ λμ μ λ€λ¦­μ μμλ₯Ό κΈ°λ°μΌλ‘ μ λ€λ¦­ νμμ μκ²λ¨
- anyμμ μ°¨μ΄μ  : νμμ€ν¬λ¦½νΈμ νμ μ²΄μ»€λ‘λΆν° λ³΄νΈλ₯Ό λ°μ μ μμ(anyλ λͺ»λ°μ)
  - μ°λ¦¬κ° νλ μμ²­μ λ°λΌ call signatureλ₯Ό μμ±ν¨

```typescript
type SuperPrint = <T, M>(a: T[], b: M) => T;
```
