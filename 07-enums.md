
## 07-enums.md

# Enums in TypeScript

Enums (**Enumerations**) are a way to define a set of named constants.  
They make code **more readable** and **manageable** when you have fixed sets of values.

---

## 1. Numeric Enums (Default)

- By default, enums are **numeric** and start at `0`.

```ts
enum Direction {
  Up,    // 0
  Down,  // 1
  Left,  // 2
  Right  // 3
}

let move: Direction = Direction.Up;
console.log(move); // Output: 0
```

## 2. Numeric Enums (Custom Values)

 - You can assign custom numbers. The rest auto increment.

 ```ts
 enum Status {
  Success = 1,
  Error,     // 2
  Pending,   // 3
}

console.log(Status.Success); // 1
console.log(Status.Error);   // 2
```
 - Useful when values needs to start from a specific number (`Like HTTP codes`).


## 3. String Enums
 - Enum Members can also be strings.

```ts
 enum Roles {
  Admin = "ADMIN",
  User = "USER",
  Guest = "GUEST"
}

let role: Roles = Roles.Admin;
console.log(role); // "ADMIN"
```
- String enums give meaningful names instead of numbers.


## 4. Heterogeneous Enums (Mix of string & Number)

 - You can mix string and number values (not recommended, but possible).

 ```ts
 enum Mixed {
  No = 0,
  Yes = "YES"
}

console.log(Mixed.No);  // 0
console.log(Mixed.Yes); // "YES"
```


## 5. Reverse Mapping (Only for Numeric Enums)

- Numeric enums create a reverse mapping (value → name).

```ts
enum Direction {
  Up = 1,
  Down,
}

console.log(Direction.Up);      // 1
console.log(Direction[1]);      // "Up" (reverse mapping)
```

- ❌ String enums don’t support reverse mapping.


## 6. const enum (Faster & Optimized)

- If you mark an enum as const, TypeScript replaces its usage with literal values at compile-time.

```ts

const enum Colors {
  Red,
  Green,
  Blue
}

let myColor = Colors.Green;
console.log(myColor); // Output: 1
```

- No extra objects is created ar runtime.


## 7. Enum in Functions

- Enums are useful in conditions or function parameters.

```ts
enum LogLevel {
  Info,
  Warning,
  Error
}

function logMessage(level: LogLevel, message: string) {
  if (level === LogLevel.Error) {
    console.error("Error:", message);
  } else {
    console.log("Log:", message);
  }
}

logMessage(LogLevel.Warning, "This is a warning");
```

