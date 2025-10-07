
## 13-modules.md

## TypeScript Modules

- A module in TypeScript is a file that contains its own scope.
By default, every TypeScript file is a module if it has at least one `import` or `export`.
Modules help you split code into smaller, reusable, maintainable parts.

#### Types of Modules
- Named exports → multiple exports per file.

- Default exports → one main export per file.

- Re-exports → combine and simplify imports.


 ### Why use Modules ?

- Organize large projects into smaller files.

- Avoid name conflicts (everything inside a module   has its own scope).

- Reuse code across multiple files. 


###   Example 1: Exporting and Importing  

- `mathUtils.ts` 

```ts
// Exporting functions (named exports)
export function add(a: number, b: number): number {
  return a + b;
}

export function multiply(a: number, b: number): number {
  return a * b;
}

// Exporting a variable
export const PI = 3.14159;
```


- `Main.ts`

```ts
// Importing named exports
import { add, multiply, PI } from "./mathUtils";

console.log("Addition:", add(5, 3)); // 8
console.log("Multiplication:", multiply(5, 3)); // 15
console.log("Value of PI:", PI); // 3.14159
```


### Example 2. Default Export 

- `Greets.js`

```ts
// Default export (only one allowed per file)
export default function greet(name: string): string {
  return `Hello, ${name}!`;
}
```


- `app.ts`

```ts
// Importing default export
import greet from "./greet";

console.log(greet("Eswar")); // "Hello, Eswar!"
```


###   Example 3: Exporting a class 

- `User.ts`

```ts
export class User {
  constructor(public name: string, public age: number) {}

  display(): void {
    console.log(`Name: ${this.name}, Age: ${this.age}`);
  }
}
```

- `index.ts`

```ts

import { User } from "./User";

const user1 = new User("Eswar", 23);
user1.display(); // Name: Eswar, Age: 23
```


### Example 4: Re-exporting (Barrel Exports)

- Sometimes you combine exports from multiple files into one.

- `math/index.ts`


```ts
export * from "./add";
export * from "./multiply";
```

`main.ts`

```ts
// Now import from index.ts
import { add, multiply } from "./math";

console.log(add(2, 3)); // 5
console.log(multiply(2, 3)); // 6
```


