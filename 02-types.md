## 02-types.md

# TypeScript Types

# Primitive Types 

- `string` → Text values  
```
  let name: string = "Eswar";
```
- `number` → Numeric values (integers, floats)
```
   let age: number = 22;
```
- `boolean` → True or False values
```
  let isActive: boolean = true;
```
- `any` → Can hold any type (not recommended)
```
  let data: any = "Hello";
```
- `unknown` → Similar to any, but safer
```
   let input: unknown = 5;
```
- `void` → Represents no value (used in functions)
```
   function log(): void {
   console.log("Hi");
   }
```
- `null` → Null value
```
  let value: null = null;
```
- `undefined` → Undefined value
```
  let value: undefined;
```
- `never` → Represents values that never occur
```
  function error(): never {
  throw new Error("Fail");
  }
```

## Non Primitive Types

### Type Arrays 
```
- `Array` of specific type  
let numbers: number[] = [1, 2, 3];
let fruits: string[] = ["Apple", "Banana"];
```
- `Using generic syntax` 
```
   let numberGeneric : Array <number> = [1,2,3];
```


### Typescript Tuple
```
- Fixed length and types
  let user : [string,number] = ["Eswar", 22];
```

### TypeScript Enum

- Named constants
```
  enum Color {
  Red,
  Green,
  Blue
  }

  let c : Color = Color.Green;
```
### TypeScript Object Types

- Object with specific Structure
```
  let person: { name: string; age: number } = { name: "Eswar", age: 22 };
```

### TypeScript Function Types
```
- Function with typed parameter and return value

  function add(a: number, b: number): number {
  return a + b;
}
```

### Union & Intersection Types
```
- Union (one of mutiple types)

  let id: string | number;
  id = "123";
  id = 456;
```
- Intersection (Combines multiple types)
```
   type A = { name: string };
   type B = { age: number };
   let person: A & B = { name: "Eswar", age: 22 };
```

### Literal Types

- Variable can have exact values only
```
   let direction: "up" | "down";
   direction = "up"; 
```

 ### Type Aliases

 - Custom type names 
```
   type User = { name: string; age: number };
   let person: User = { name: "Eswar", age: 22 };
```
 ### Advanced Types 

 - Generics (reusable for multiple types)
```
   function identity<T>(arg: T): T {
  return arg;
  }
```

### Type Assertions (tell TypeScript the type)

- let value: any = "Hello";
```
  let length: number = (value as  string).length;
```





