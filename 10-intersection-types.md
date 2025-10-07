
## 10-intersection-types.md

An **Intersection Type** combines **multiple types into one**.  
It means that the variable/object **must include all the properties** from the combined types.

The syntax uses the `&` symbol.

---

## 1. Basic Intersection

```ts
type Person = { name: string };
type Employee = { id: number };

type Staff = Person & Employee;

let staffMember: Staff = {
  name: "Alice",
  id: 101
};
```

- Here, `Staff` must have both `name` and `id`.



## 2. Multiple Intersections

- You can combine more than two types.

```ts
type A = { a: string };
type B = { b: number };
type C = { c: boolean };

type ABC = A & B & C;

let obj: ABC = {
  a: "Hello",
  b: 42,
  c: true
};
```

- The object must satisfy all three types.


## 3. Intersection with Functions

```ts
type Logger = (message: string) => void;
type Formatter = (input: string) => string;

type LogFormatter = Logger & Formatter;

// Example implementation
const logAndFormat: LogFormatter = (msg: string) => {
  console.log("Log:", msg);
  return msg.toUpperCase();
};

console.log(logAndFormat("hello")); // HELLO
```

- The function must fulfill `both contracts`.




## 4. Intersection with Unions

```ts

type Admin = { role: "admin"; permissions: string[] };
type User = { name: string };

type SuperUser = Admin & User;

let superAdmin: SuperUser = {
  role: "admin",
  permissions: ["read", "write"],
  name: "Bob"
};
```

- `SuperUser` is both an `Admin` and a `User`.




## 5. Conflict in Intersections

- If types define the same property with different types, it causes an error.

```ts
type A = { value: string };
type B = { value: number };

type AB = A & B;

// let obj: AB = { value: "test" }; // ❌ Error
// let obj: AB = { value: 123 };    // ❌ Error
```

- This makes `value` type become `never`, since it can’t be both `string` and `number`.



## Real world Example 

```ts

type Address = {
  city: string;
  zip: number;
};

type Contact = {
  email: string;
  phone: string;
};

type Customer = Address & Contact;

let customer: Customer = {
  city: "New York",
  zip: 10001,
  email: "test@example.com",
  phone: "123-456-7890"
};
```

- `Customer` combines both `Address` and `Contact`.



