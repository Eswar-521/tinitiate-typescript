
## 14-namespaces.md


### TypeScript Namespaces

- A namespace in TypeScript is a way to organize related code (functions, classes, interfaces, variables) under a single name to avoid name conflicts.

Namespaces are mainly used in older TypeScript/JavaScript codebases (before ES Modules became standard).
Now we mostly use modules, but namespaces are still useful in some projects.



### Why use Namespaces ?

- Group related code together.

- Prevent name collisions (two files having same function names).

- Helpful in large applications.


### Example 1: Basic Namespace


```ts


namespace MathUtils {
  export function add(a: number, b: number): number {
    return a + b;
  }

  export function multiply(a: number, b: number): number {
    return a * b;
  }
}

// Using the namespace
console.log(MathUtils.add(5, 3));      // 8
console.log(MathUtils.multiply(5, 3)); // 15
```

- Here, `add` and `multiply` are inside MathUtils.
We must use export inside namespaces to access them outside.


###   Example 2. Nested Namespaces 

```ts

namespace Company {
  export namespace HR {
    export class Employee {
      constructor(public name: string, public id: number) {}
      display(): void {
        console.log(`Employee: ${this.name}, ID: ${this.id}`);
      }
    }
  }

  export namespace Finance {
    export function calculateSalary(base: number, bonus: number): number {
      return base + bonus;
    }
  }
}

// Using nested namespaces
const emp = new Company.HR.Employee("Eswar", 101);
emp.display(); // Employee: Eswar, ID: 101

console.log(Company.Finance.calculateSalary(30000, 5000)); // 35000
```


### Example 3. Splitting Namespaces Across Files 

- You can spread one namespace into multiple files.

`MathUtilsl.ts`

```ts
namespace MathUtils {
  export function subtract(a: number, b: number): number {
    return a - b;
  }
}
```

```MathUtils2.ts`

```ts
namespace MathUtils {
  export function divide(a: number, b: number): number {
    return a / b;
  }
}
```


`main.ts`

```ts
/// <reference path="MathUtils1.ts" />
/// <reference path="MathUtils2.ts" />

console.log(MathUtils.subtract(10, 5)); // 5
console.log(MathUtils.divide(10, 2));   // 5
```


### Example 4. Namespaces with Interfaces 

```ts

namespace Shapes {
  export interface Shape {
    area(): number;
  }

  export class Circle implements Shape {
    constructor(public radius: number) {}
    area(): number {
      return Math.PI * this.radius * this.radius;
    }
  }
}

const c = new Shapes.Circle(5);
console.log("Circle Area:", c.area()); // Circle Area: 78.54
```

- Namespaces = organize code within one global scope (old approach).

- Modules = organize code across multiple files with imports/exports (modern approach, preferred).
