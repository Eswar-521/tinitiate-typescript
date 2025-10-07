
## 05-classes.md

# TypeScript Classes

## What is a Class?

A **class** in TypeScript is a blueprint for creating objects.  
It can contain **properties**, **methods**, and **constructors**.  
TypeScript adds **type safety** and **access modifiers** to classes.

---

## Basic Class

```ts
class Person {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  greet() {
    console.log(`Hello, my name is ${this.name} and I am ${this.age} years old`);
  }
}

let person1 = new Person("Eswar", 22);
person1.greet(); 
//  ==> Output: Hello, my name is Eswar and I am 22 years old

```

 - `constructor` → special method called when creating an instance.
 - `this` → refers to the current object.

## Access Modifiers

### TypeScript supports three access modifiers
 - `public` → default, accessible anywhere

 - `private` → accessible only inside the class

 - `protected` → accessible inside class and      subclasses

```ts
class Person {
  public name: string;
  private age: number;
  protected gender: string;

  constructor(name: string, age: number, gender: string) {
    this.name = name;
    this.age = age;
    this.gender = gender;
  }

  getAge() {
    return this.age; // can access private inside class
  }
}

let person = new Person("Eswar", 22, "Male");
console.log(person.name); // ✅ public
console.log(person.getAge()); // ✅ access private via method
===> // console.log(person.age); // ❌ Error: private
===> // console.log(person.gender); // ❌ Error: protected
```
## Readonly Properties
 - `readonly` properties cannot be changed after initialization

```ts
class Person {
  readonly id: number;
  name: string;

  constructor(id: number, name: string) {
    this.id = id;
    this.name = name;
  }
}

let p = new Person(1, "Eswar");
p.name = "New Name"; 
 ===> // p.id = 2; // ❌ Error: readonly
```
## Inheritance (Extending Class)

 - Classes can inherit from another class using extends.

 ```ts
 class Person {
  name: string;
  constructor(name: string) {
    this.name = name;
  }
  greet() {
    console.log(`Hello, my name is ${this.name}`);
  }
}

class Employee extends Person {
  employeeId: number;
  constructor(name: string, employeeId: number) {
    super(name); // call parent constructor
    this.employeeId = employeeId;
  }
  showId() {
    console.log(`Employee ID: ${this.employeeId}`);
  }
}

let emp = new Employee("Eswar", 101);
emp.greet();   // Hello, my name is Eswar
emp.showId();  // Employee ID: 101
```

## Getters and Setters

- Allows controlled access to properties

```ts
class Person {
  private _age: number;

  constructor(age: number) {
    this._age = age;
  }

  get age(): number {
    return this._age;
  }

  set age(value: number) {
    if (value < 0) throw new Error("Age cannot be negative");
    this._age = value;
  }
}

let person = new Person(22);
console.log(person.age); // 22
person.age = 25;         

```

## Static Properties and Methods

 - Belong to the class, not instances

 ```ts
 class Calculator {
  static pi: number = 3.14;

  static calculateArea(radius: number): number {
    return Calculator.pi * radius * radius;
  }
}

console.log(Calculator.pi); // 3.14
console.log(Calculator.calculateArea(5)); // 78.5
```
## Abstract Classes 

 - Cannot be instantiated directly
 - Must be extended by other classes 

 ```ts
 abstract class Shape {
  abstract area(): number; // must be implemented by subclass
}

class Circle extends Shape {
  radius: number;
  constructor(radius: number) {
    super();
    this.radius = radius;
  }

  area(): number {
    return Math.PI * this.radius * this.radius;
  }
}

let c = new Circle(5);
console.log(c.area()); // 78.53981633974483
```

## Implementing Interfaces in classes

```ts
interface PersonInterface {
  name: string;
  greet(): void;
}

class Person implements PersonInterface {
  name: string;
  constructor(name: string) {
    this.name = name;
  }

  greet() {
    console.log(`Hello, my name is ${this.name}`);
  }
}

let p = new Person("Eswar");
p.greet(); // Hello, my name is Eswar
```
