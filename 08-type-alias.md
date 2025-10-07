
## 08-type-alias.md

# Type Aliases in TypeScript

A **Type Alias** in TypeScript is a way to give a **custom name** to a type.  
It makes complex types easier to read and reuse.

You create them using the `type` keyword.

---

## 1. Basic Type Alias

```ts
type ID = string | number;

let userId: ID = 101;    // number
let productId: ID = "A1"; // string
```

- Instead of repeating `string | number`, you define it once as `ID`.

## 2. Object Type Alias

- You can alias object shapes.

```ts
type User = {
  id: number;
  name: string;
  isAdmin: boolean;
};

let person: User = {
  id: 1,
  name: "John",
  isAdmin: true
};
```

- `User` can now be reused in multiple places.


## 3. Function Type Alias

- Type aliases can also describe `function signatures`.

```ts

type Add = (a: number, b: number) => number;

const addNumbers: Add = (x, y) => x + y;

console.log(addNumbers(5, 3)); // 8
```

- Ensures the function always follows the same structure.



## 4. Generic Type Aliases

- Type aliases can use generics.

```ts
type ApiResponse<T> = {
  status: number;
  data: T;
};

let userResponse: ApiResponse<{ id: number; name: string }> = {
  status: 200,
  data: { id: 1, name: "Bob" }
};
```

- Reusable for multiple data types (`User, Product`, etc.).



