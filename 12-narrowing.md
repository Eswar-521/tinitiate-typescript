
## 12-narrowing.md


**Narrowing** is the process of refining a variable's type from a **broad type** (like `unknown`, `any`, or a `union`)  
to a **more specific type** based on checks you do in your code.

👉 TypeScript uses your **runtime checks** (`typeof`, `instanceof`, property checks, etc.)  
to narrow down the type and give you better type safety.

---

## 1. Typeof Narrowing

You can use `typeof` to check primitive types.

```ts
function printValue(value: string | number) {
  if (typeof value === "string") {
    console.log("String value:", value.toUpperCase()); // ✅ string methods allowed
  } else {
    console.log("Number value:", value.toFixed(2));   // ✅ number methods allowed
  }
}

printValue("hello");
printValue(42);
```

- Here, TypeScript narrows value to string or number depending on the branch.


## 2. Truthiness Narrowing

- TypeScript uses truthy/falsy checks to narrow types.

```ts

function printMessage(msg?: string) {
  if (msg) {
    console.log("Message:", msg.toUpperCase()); // ✅ msg is string
  } else {
    console.log("No message");
  }
}

printMessage("Hi");
printMessage();
```
- Inside the if `(msg)` block, TS knows `msg` is not `undefined`.




## 3. Equality Narrowing

- Comparisons (`===`, `!==`) help refine types.


```ts
function compare(x: string | number, y: string | boolean) {
  if (x === y) {
    // Both must be string here
    console.log(x.toUpperCase());
  } else {
    console.log("Not equal");
  }
}
```

- If `x === y`, both must be `string`.



## 4. Instanceof Narrowing


- For class-based objects, use `instanceof`.


```ts
class Dog {
  bark() { console.log("Woof!"); }
}

class Cat {
  meow() { console.log("Meow!"); }
}

function makeSound(animal: Dog | Cat) {
  if (animal instanceof Dog) {
    animal.bark(); // ✅ narrowed to Dog
  } else {
    animal.meow(); // ✅ narrowed to Cat
  }
}
```

## 5. In Operator Narrowing

- Check if an object has a property.

```ts 

type Car = { drive: () => void };
type Boat = { sail: () => void };

function move(vehicle: Car | Boat) {
  if ("drive" in vehicle) {
    vehicle.drive(); // ✅ Car
  } else {
    vehicle.sail();  // ✅ Boat
  }
}
```

## 6. Discriminated Unions

- Using a common literal property (`kind`) makes narrowing very powerful.

```ts
type Circle = { kind: "circle"; radius: number };
type Square = { kind: "square"; side: number };

type Shape = Circle | Square;

function area(shape: Shape) {
  if (shape.kind === "circle") {
    return Math.PI * shape.radius ** 2;
  } else {
    return shape.side * shape.side;
  }
}

console.log(area({ kind: "circle", radius: 5 }));
```

- The `kind` property helps TS know exactly which shape it is.



## 7. Exhaustiveness Checking with never

- Ensures all cases are handled.

```ts

function getArea(shape: Shape): number {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;
    case "square":
      return shape.side * shape.side;
    default:
      const _exhaustive: never = shape; // ❌ Error if new kind added
      return _exhaustive;
  }
}
```

- Prevents missing cases when new union members are added.
