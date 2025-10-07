
## 09-union-types.md


A **Union Type** allows a variable to hold **more than one type**.  
It’s written using the `|` (pipe) symbol.

This makes code more **flexible** while still being **type-safe**.

---

## 1. Basic Union Type

```ts
let value: string | number;

value = "Hello"; // ✅ string allowed
value = 42;      // ✅ number allowed
// value = true; // ❌ Error (boolean not allowed)
```
- The variable value can be string or number, but nothing else.


## 2. Union in Functions

- Functions can accept multiple types for parameters.

```ts

function printId(id: string | number) {
  console.log("ID:", id);
}

printId(101);      // ✅ number
printId("A123");   // ✅ string
```
- Useful for handling flexible inputs (like user IDs that may be string or number).



## 3. Type Narrowing with Unions

- When using unions, you often need to check the type before using it.
This is called type narrowing.

```ts
function getLength(value: string | number): number {
  if (typeof value === "string") {
    return value.length; // ✅ allowed (string has length)
  } else {
    return value;        // ✅ here it's number
  }
}

console.log(getLength("Hello")); // 5
console.log(getLength(10));      // 10
```

- TypeScript automatically narrows the type inside conditions.


## 4. Union with Objects

```ts
type Dog = { type: "dog"; bark: () => void };
type Cat = { type: "cat"; meow: () => void };

type Pet = Dog | Cat;

function makeSound(pet: Pet) {
  if (pet.type === "dog") {
    pet.bark();
  } else {
    pet.meow();
  }
}
```

- Here `Pet` can be either a `Dog` or a `Cat`.


## 5. Union with Type Aliases
- You can define a custom union type using `type`.

```ts
type Status = "success" | "error" | "pending";

let response: Status;

response = "success"; // ✅ valid
response = "error";   // ✅ valid
// response = "failed"; // ❌ Error
```
- ✅ This ensures `response` can only be one of the allowed string literals.



## 6. Array with Union Types

- You can use unions inside arrays.

```ts
let data: (string | number)[] = [1, "two", 3, "four"];

console.log(data); // [1, "two", 3, "four"]
```

- The array can hold both numbers and strings.


## 7. Union with null or undefined

- Unions can be used to allow `null` or `undefined` values.


```ts
let username: string | null;

username = "Alice"; // ✅
username = null;    // ✅
```

- Useful for handling optional values safely.

