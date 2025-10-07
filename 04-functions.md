
## 04-functions.md

## What is a Function?

A **function** is a block of code designed to perform a task.  
In TypeScript, functions can have **typed parameters** and **typed return values**, which helps catch errors at compile time.

---

## Basic Function

```ts
function add(a: number, b: number): number {
  return a + b;
}

let result = add(5, 3); // ==> result = 8

```

##  Function with Optional Parameter 

### This is the Parameter Function

```ts
function greet(name: string, age?: number): string {
  if (age) {
    return `Hello ${name}, you are ${age} years old`;
  }
  return `Hello ${name}`;
}

greet("Eswar");      ==>  // Hello Eswar
greet("Eswar", 22);   ==> // Hello Eswar, you are 22 years old

```



## Function with Default Parameter 

```ts
function greet(name: string, age: number = 18): string {
  return `Hello ${name}, you are ${age} years old`;
}

greet("Eswar");       // Hello Eswar, you are 18 years old
greet("Eswar", 22);   // Hello Eswar, you are 22 years old
```
- `age` : number = 18 → default value 


## Function With Rest Parameter 

```ts
function sum(...numbers: number[]): number {
  return numbers.reduce((acc, val) => acc + val, 0);
}

sum(1, 2, 3, 4); // 10

```

 - `...numbers: number[]` → accepts multiple arguments as an array


## Anoymous Function 

```ts
let multiply = function(a: number, b: number): number {
  return a * b;
};

multiply(5, 3); // 15
```


## Arrow Function 

- let divide = (a: number, b: number): number => a / b;

divide(10, 2); 

## Function Type 

- You can define a variable type for a function:

```ts
let add: (x: number, y: number) => number;

add = (a, b) => a + b;
```
- `(x: number, y: number)` => number → function type signature


## Function Overloading 

- Define multiple signatures for a function:

```ts
function combine(a: number, b: number): number;
function combine(a: string, b: string): string;
function combine(a: any, b: any): any {
  return a + b;
}

combine(1, 2);       // 3
combine("Hello", " World"); // ==> Hello World 
```

