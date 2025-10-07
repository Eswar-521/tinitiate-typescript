
## 11-type-assertion.md


**Type Assertion** tells TypeScript to **treat a value as a specific type**.  
It doesn’t change the actual runtime value, but helps TypeScript understand the type better.

👉 Think of it like telling the compiler:  
*"Trust me, I know the type of this value."*

---

## 1. Basic Type Assertion

Two syntaxes are available: `as` and `<>`.

```ts
let value: unknown = "Hello World";

// Using `as`
let strLength1: number = (value as string).length;

// Using `<>` (not recommended in JSX/React)
let strLength2: number = (<string>value).length;

console.log(strLength1); // 11
console.log(strLength2); // 11

```

- Here, we assert that `value` is a `string`.


## 2. DOM Manipulation Example


Often used with DOM elements (because `document.getElementById` returns `HTMLElement | null`).


```ts

let input = document.getElementById("username") as HTMLInputElement;

input.value = "Eswar"; // ✅ Now we can access `.value`
```

- Without assertion, TypeScript won’t know that `input` is a text box.

## 3. Type Assertion with Union Types


- Sometimes you have a union and want to assert a more specific type.

```ts
type Bird = { fly: () => void };
type Fish = { swim: () => void };

function move(animal: Bird | Fish) {
  if ("fly" in animal) {
    (animal as Bird).fly();
  } else {
    (animal as Fish).swim();
  }
}
```

- Here we tell TypeScript whether it’s a `Bird` or `Fish`.


## 4. Non-Null Assertion (!)
 

- If you’re sure a value is `not null or undefined`, you can use !.

```ts
let element = document.querySelector("div")!;
element.innerHTML = "Hello!";
```

- The `!` tells TypeScript "this will never be null."

