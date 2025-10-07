
## 15-decorators.md

### TypeScript Decorators 

- A decorator is a special kind of declaration that can be attached to a class, method, property, or parameter to modify its behavior.

They are basically functions that receive metadata about the thing they decorate.

- Think of them as annotations or wrappers that add extra behavior.

- Note: To use decorators, you must enable them in tsconfig.json:

```ts

{
  "compilerOptions": {
    "experimentalDecorators": true
  }
}
```

## Types of Decorators 
- Class Decorators → modify classes.

- Method Decorators → modify methods.

- Property Decorators → modify properties.

- Parameter Decorators → modify function parameters.


### Why use Decorator

- Add extra behavior without changing original code.

- Useful in frameworks like Angular (e.g., `@Component`, `@Injectable`).

- Clean and reusable.



### Example 1. Class Decorator 

```ts

// A simple class decorator
function Logger(constructor: Function) {
  console.log("Logging class:", constructor.name);
}

@Logger
class User {
  constructor(public name: string) {}
}

// When class is declared → "Logging class: User"
const u = new User("Eswar");
```

- Here, `@Logger` runs when the class is defined, not when it’s instantiated.


### Example 2.Class Decorator with Behavior


```ts
function AddCreatedAt(constructor: Function) {
  constructor.prototype.createdAt = new Date();
}

@AddCreatedAt
class Product {
  name: string;
  constructor(name: string) {
    this.name = name;
  }
}

const p: any = new Product("Laptop");
console.log(p.name);       // Laptop
console.log(p.createdAt);  // Date object
```

- The decorator adds a new property `createdAt` to every instance.



###   Example 3. Method Decorator

```ts
function LogMethod(
  target: any,
  propertyName: string,
  descriptor: PropertyDescriptor
) {
  const originalMethod = descriptor.value;

  descriptor.value = function (...args: any[]) {
    console.log(`Method ${propertyName} called with:`, args);
    return originalMethod.apply(this, args);
  };
}

class Calculator {
  @LogMethod
  add(a: number, b: number) {
    return a + b;
  }
}

const calc = new Calculator();
console.log(calc.add(5, 3)); // Logs: Method add called with: [5, 3] → 8
```

- `@LogMethod` wraps the original method to log calls before executing.




### Example 4. Property Decorator

```ts

function ReadOnly(target: any, propertyName: string) {
  Object.defineProperty(target, propertyName, {
    writable: false
  });
}

class Car {
  @ReadOnly
  brand: string = "Tesla";
}

const c = new Car();
c.brand = "BMW"; // ❌ Error in strict mode
console.log(c.brand); // Tesla
```

- `@ReadOnly` makes the property `immutable`.



### Example 5. Parameter Decorator

```ts
function LogParameter(target: any, methodName: string, parameterIndex: number) {
  console.log(
    `Parameter in ${methodName} at index ${parameterIndex} is decorated.`
  );
}

class Person {
  greet(@LogParameter message: string) {
    console.log(message);
  }
}

// Logs: Parameter in greet at index 0 is decorated.
const p = new Person();
p.greet("Hello!");
```



