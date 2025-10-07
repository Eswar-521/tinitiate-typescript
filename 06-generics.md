
## 06-generics.md

## Generics in TypeScript

Generics allow you to create reusable components that can work with **different types**  
instead of being restricted to a single one.

They help in writing flexible, reusable, and type-safe code.

---

## Generic Function

- A function that works with different types without losing type safety.


```ts
function identity<T>(value: T): T {
  return value;
}

let num = identity<number>(10);   // T is number
let str = identity<string>("Hello"); // T is string

```
 - Here <T> is a type parameter that can represent any type.



## Generic with Multiple Parameters


- You can use more than one type parameter.
```ts
function pair<K, V>(key: K, value: V): [K, V] {

  return [key, value];

}

```
 - let result = pair<string, number>("Age", 25); //  
 [string, number]

 - <K, V> represents two different types.



## Generic Interfaces 

 - Interfaces can use generics to define flexible structures.

 ```ts
 interface Box<T> {
  value: T;
}

let stringBox: Box<string> = { value: "Hello" };
let numberBox: Box<number> = { value: 123 };
```

- The same Box interface works with both `string` and `number`.


## Generic Classes 
 - Classes can also be generic

 ```ts
 class DataStore<T> {
  private data: T[] = [];

  add(item: T): void {
    this.data.push(item);
  }

  getAll(): T[] {
    return this.data;
  }
}

let numberStore = new DataStore<number>();
numberStore.add(10);
numberStore.add(20);

let stringStore = new DataStore<string>();
stringStore.add("Apple");
stringStore.add("Banana");
```
- `DataStore` can store any type (`number`, `string`, ect...)

## Generic Constraints (`Extends`)

```ts

function getLength<T extends { length: number }>(item: T): number {
  return item.length;
}

console.log(getLength("Hello"));    // Works (string has length)
console.log(getLength([1, 2, 3]));  // Works (array has length)
// console.log(getLength(123));     // ❌ Error (number has no length)
```
 - One type with a length property are allowed.

 ## Default Type for Generics

 - You can assign a default type if no type is provided.

 ```ts
 function createValue<T = string>(value: T): T {
  return value;
}

let a = createValue("Hello"); // T = string (default)
let b = createValue(100);     // T = number (overrides default)
```


## Using `keyof` with Generics 

- Helps to ensure safe access to object properties.

```ts
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

let person = { name: "John", age: 30 };

let nameValue = getProperty(person, "name"); // string
let ageValue = getProperty(person, "age");   // number
// getProperty(person, "salary");            // ❌ Error (salary doesn't exist)
```

