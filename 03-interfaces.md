
# 03-interfaces.md

## TypeScript Interfaces

## What is an Interface?

An **interface** in TypeScript is a way to define the **structure of an object**. It specifies what properties and methods an object should have, without implementing them.  
Interfaces help with **type checking** and **code consistency**.

---

## Basic Interface Example

```ts
interface Person {
  name: string;
  age: number;
}

let employee: Person = {
  name: "Eswar",
  age: 22
};
```


## optional Properties

- You can make properties optional Using..?

```ts
interface Person {
  name: string;
  age?: number; // => this is Optional
}

let user: Person = { name: "Eswar" }; 

age is Optional 

```

## Readonly Properties 

 - Use readonly to prevent property modification 

 ```ts
 interface Person {
  readonly id: number;
  name: string;
}

let user: Person = { id: 1, name: "Eswar" };
user.id = 2; // => ❌ Error: cannot assign to 'id'
```

## Functions in Interface

```ts
interface Calculator {
  add(a: number, b: number): number;
  subtract(a: number, b: number): number;
}

let calc: Calculator = {
  add: (x, y) => x + y,
  subtract: (x, y) => x - y
};
```

## Extending InterFaces 

 - One interface can extend another

 ```ts
 interface Person {
  name: string;
  age: number;
}

interface Employee extends Person {
  employeeId: number;
}

let emp: Employee = {
  name: "Eswar",
  age: 22,
  employeeId: 101
};
```

## Indexable Types

 - Interfaces can describe array-like or object like structures

 ```ts
 interface StringArray {
  [index: number]: string;
}

let fruits: StringArray = ["Apple", "Banana"];
```

## Implementing Interfaces in Classes

```ts
interface Person {
  name: string;
  greet(): void;
}

class Employee implements Person {
  name: string;
  constructor(name: string) {
    this.name = name;
  }

  greet() {
    console.log(`Hello, my name is ${this.name}`);
  }
}

let emp = new Employee("Eswar");
emp.greet(); // => Hello, my name is Eswar
```

