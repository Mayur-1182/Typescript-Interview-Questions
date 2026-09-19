# TypeScript Interview Practice — Questions & Interview-Ready Answers

## Question 1 — `type` vs `interface`

### Question
What is the difference between `type` and `interface` in TypeScript? When would you prefer one over the other?

### Interview-ready answer
`type` and `interface` are both used to define custom types in TypeScript. I prefer `interface` when I'm defining an object structure that may need to be extended or declaration merging. I prefer `type` when I need union types, intersection types, primitive aliases, tuples, or more complex type compositions. Interfaces are especially useful when there is a clear object-oriented or inheritance-style relationship between shapes.

### Example

```ts
interface User {
  name: string;
}

interface Admin extends User {
  role: string;
}

type Status = "success" | "error";
```

### Key correction
- Interfaces are not only for objects, but they are especially suited to object-like shapes.
- Declaration merging is supported by `interface`, not by `type` aliases.

---

## Question 2 — `any`, `unknown`, and `never`

### Question
What is the difference between `any`, `unknown`, and `never`?

### Interview-ready answer
`any` disables TypeScript's type checking for that value, so I can perform almost any operation on it. `unknown` is used when I don't know the type yet, but unlike `any`, I must narrow or validate the value before using it. `never` represents a value that can never be produced because the code path never completes normally, such as a function that always throws or loops forever.

### Examples

```ts
let a: any = "hello";
a.foo.bar(); // TypeScript allows it

let b: unknown = "hello";
// b.toUpperCase(); // Error

if (typeof b === "string") {
  b.toUpperCase();
}

function fail(message: string): never {
  throw new Error(message);
}
```

### Key correction
Do not say `never` means "the value will never exist." It means the function/expression cannot successfully produce a value or complete normally.

### Memory hook
- `any` → "Don't type-check this."
- `unknown` → "I don't know yet; prove the type first."
- `never` → "This code path cannot return normally."

---

## Question 3 — Type narrowing

### Question
What is type narrowing in TypeScript? Give at least three ways to narrow a type.

### Interview-ready answer
Type narrowing is the process of reducing a broader type to a more specific type based on runtime checks. It is commonly used with union types and `unknown`.

### Example

```ts
type Value = number | string;

function process(value: Value) {
  if (typeof value === "string") {
    value.trim();
  } else {
    value.toFixed(2);
  }
}
```

### Common narrowing techniques

#### `typeof`
Used mainly for primitive types.

```ts
if (typeof value === "string") {
  // value is string
}
```

#### `instanceof`
Used for class or built-in object instances.

```ts
if (value instanceof Date) {
  // value is Date
}
```

#### `in`
Used to check whether a property exists.

```ts
if ("name" in user) {
  // user has name
}
```

### Key correction
Narrowing is not limited to union types. It can also narrow `unknown`, nullable types, and discriminated unions.

---

## Question 4 — `extends`, intersection `&`, and union `|`

### Question
What is the difference between interface `extends`, type intersection (`&`), and union (`|`)?

### Interview-ready answer
`extends` lets one interface inherit the properties of another interface. Intersection `&` combines multiple types so the result must satisfy all of them. Union `|` means a value can be one of several possible types.

### Examples

```ts
interface User {
  name: string;
}

interface Admin extends User {
  role: string;
}
```

`Admin` contains both `name` and `role`.

```ts
type User = {
  name: string;
};

type Employee = {
  salary: number;
};

type EmployeeUser = User & Employee;
```

`EmployeeUser` must contain both `name` and `salary`.

```ts
let value: string | number;

value = "hello";
value = 100;
```

### Key correction
Do not describe `extends` and `&` as exactly the same. They can produce similar object shapes, but `extends` expresses interface inheritance while `&` creates an intersection type.

---

## Question 5 — Generics

### Question
What are generics in TypeScript? Why are they different from `any`?

### Interview-ready answer
Generics let us create reusable code while preserving the relationship between input and output types. Unlike `any`, generics keep type information instead of removing type checking.

### Example

```ts
function identity<T>(value: T): T {
  return value;
}

const a = identity("hello"); // string
const b = identity(100);     // number
```

We can also explicitly provide the type:

```ts
identity<number>(100);
```

### Generic constraint example

```ts
function value<T extends number | string | boolean>(value: T): T {
  return value;
}
```

Here `T` is restricted to `number`, `string`, or `boolean`.

### Key correction
The correct constraint syntax is:

```ts
<T extends SomeType>
```

not:

```ts
<T>(value: T extends SomeType)
```

---

## Question 6 — Generic constraints

### Question
Why does this fail?

```ts
function getLength<T>(value: T) {
  return value.length;
}
```

How do you fix it with a generic constraint?

### Interview-ready answer
An unconstrained generic can represent any type, so TypeScript cannot guarantee that `T` has a `length` property. I can add a generic constraint to require that `T` has a numeric `length` property.

### Correct solution

```ts
function getLength<T extends { length: number }>(value: T) {
  return value.length;
}
```

Now all of these can work:

```ts
getLength("hello");
getLength([1, 2, 3]);
getLength({ length: 10 });
```

But these fail:

```ts
getLength(123);
getLength(true);
```

### Interview point
Generic constraints let us say:

> "T can be many different types, but it must satisfy this minimum structure."

---

## Question 7 — Generic vs `any`

### Question
Why is this better than using `any`?

```ts
function getValue<T>(value: T): T {
  return value;
}
```

### Interview-ready answer
A generic preserves the relationship between the input and output types. If the input is a string, TypeScript knows the return value must be a string. With `any`, that relationship is lost because `any` disables meaningful type safety.

### Example

```ts
function identity<T>(value: T): T {
  return value;
}

const result = identity("hello");
// result: string
```

This implementation is invalid:

```ts
function identity<T>(value: T): T {
  return 123; // Error because T may be string, boolean, etc.
}
```

With `any`:

```ts
function identity(value: any): any {
  return 123;
}
```

TypeScript does not protect the caller.

### Interview phrase
> Generics preserve the input-output type relationship; `any` removes that safety.

---

## Question 8 — `void`, `undefined`, and `never`

### Question
What is the difference between `void`, `undefined`, and `never`?

### Interview-ready answer
`void` is commonly used for functions that do not return a useful value. `undefined` is an actual value and type. `never` means the function or code path can never complete normally and therefore never returns a value.

### Examples

```ts
function logMessage(message: string): void {
  console.log(message);
}
```

```ts
let value: undefined = undefined;
```

```ts
function fail(message: string): never {
  throw new Error(message);
}
```

### Memory hook
- `void` → no useful return value
- `undefined` → actual `undefined` value
- `never` → no normal completion

---

## Question 9 — Optional, `readonly`, and non-null assertion

### Question
What is the difference between `?`, `readonly`, and `!`?

### Interview-ready answer
An optional property using `?` may be missing. `readonly` prevents reassignment of that property through TypeScript's type system. The non-null assertion operator `!` tells TypeScript that I am sure a value is not `null` or `undefined`.

### Example

```ts
interface User {
  name?: string;
  readonly id: number;
}
```

Optional:

```ts
const user: User = { id: 1 };
```

Readonly:

```ts
user.id = 2; // Error
```

Non-null assertion:

```ts
user.name!.toUpperCase();
```

### Important warning
`!` does not perform a runtime check. If the value is actually `undefined`, the program can still fail at runtime.

---

## Question 10 — Discriminated unions

### Question
What is a discriminated union?

### Interview-ready answer
A discriminated union is a union of object types that share a common property called the discriminant. Each possible literal value of that property identifies a specific object shape, and TypeScript uses it for type narrowing.

### Example

```ts
type Success = {
  status: "success";
  data: string;
};

type ErrorResponse = {
  status: "error";
  message: string;
};

type Response = Success | ErrorResponse;
```

```ts
function handleResponse(response: Response) {
  if (response.status === "success") {
    console.log(response.data);
  } else {
    console.log(response.message);
  }
}
```

Here `status` is the discriminant.

### Interview phrase
> The discriminant lets TypeScript know which member of the union I am working with.

---

## Question 11 — Utility types

### Question
What are `Partial<T>`, `Required<T>`, `Pick<T, K>`, and `Omit<T, K>`?

### Interview-ready answer
These are built-in TypeScript utility types used to transform existing types without rewriting them. `Partial` makes all properties optional, `Required` makes them required, `Pick` selects specific properties, and `Omit` removes specific properties.

### Examples

```ts
interface User {
  name: string;
  age?: number;
}
```

```ts
type PartialUser = Partial<User>;
```

```ts
type RequiredUser = Required<User>;
```

```ts
type UserPreview = Pick<User, "name">;
```

```ts
type UserWithoutAge = Omit<User, "age">;
```

### Correction
These are **utility types**, not union types.

---

## Question 12 — `Pick` vs `Omit`

### Question
What are the resulting types?

```ts
interface User {
  name: string;
  age: number;
  email: string;
}

type UserData = Pick<User, "name" | "email">;
type UserData2 = Omit<User, "age">;
```

### Interview-ready answer

Both result in:

```ts
{
  name: string;
  email: string;
}
```

But the mechanism differs:

- `Pick` → explicitly choose the properties you want.
- `Omit` → explicitly remove the properties you do not want.

### React example

```ts
interface User {
  id: number;
  name: string;
  email: string;
  password: string;
  role: string;
}

type UserCardProps = Omit<User, "password" | "role">;
```

This can help prevent UI components from accidentally depending on sensitive or irrelevant fields.

---

## Question 13 — Simple union vs discriminated union

### Question
Why is this:

```ts
type Status = "loading" | "success" | "error";
```

different from:

```ts
type State =
  | { status: "loading" }
  | { status: "success"; data: string }
  | { status: "error"; message: string };
```

### Interview-ready answer
A discriminated union is a union of object types that share a common property with literal values. That property is called the discriminator.

### React example

```ts
type State =
  | { status: "loading" }
  | { status: "success"; data: User[] }
  | { status: "error"; message: string };
```

This is useful for API/loading/error state because the available properties depend on the current status.

---

## Question 14 — Function overloads

### Question
What is function overload in TypeScript, and why can it be useful?

### Interview-ready answer
Function overloads let us define multiple valid call signatures for one function while keeping a single implementation. They are useful when the return type depends on the argument type.

### Example

```ts
function format(value: string): string;
function format(value: number): number;

function format(value: string | number) {
  if (typeof value === "string") {
    return value.toUpperCase();
  }

  return value * 2;
}
```

Now:

```ts
const a = format("hello"); // string
const b = format(10);      // number
```

Without overloads:

```ts
function format(value: string | number): string | number {
  // ...
}
```

the result is generally typed as `string | number`, even when the caller knows which input was passed.

### Interview phrase
> Overloads improve the API contract when different input types produce different return types.

---

## Question 15 — `const`, `readonly`, and `as const`

### Question
What is the difference between `const`, `readonly`, and `as const`?

### Interview-ready answer
`const` prevents reassignment of a variable. `readonly` prevents reassignment of a specific property through TypeScript's type system. `as const` makes an expression deeply readonly for literal inference purposes and narrows values to their literal types.

### Example

Without `as const`:

```ts
const user = {
  name: "Mayur",
  age: 25
};
```

TypeScript generally infers:

```ts
{
  name: string;
  age: number;
}
```

With `as const`:

```ts
const user = {
  name: "Mayur",
  age: 25
} as const;
```

the type is effectively:

```ts
{
  readonly name: "Mayur";
  readonly age: 25;
}
```

### Important distinction

`const` does not make object properties readonly:

```ts
const user = { name: "Mayur" };

user.name = "Rahul"; // Allowed
```

### Key correction
`as const` is not about making data reusable across the application or avoiding duplicates. Its main effect is literal type narrowing and readonly inference.

---

## Question 16 — Type assertion

### Question
What is type assertion, and does `as string` convert the runtime value?

### Interview-ready answer
Type assertion tells TypeScript to treat a value as a specific type. It changes TypeScript's static view of the value but does not convert the runtime value.

### Example

```ts
const value: unknown = "hello";

const str = value as string;
```

This tells TypeScript to treat `value` as a string.

But:

```ts
const value: unknown = 123;
const str = value as string;

console.log(str.toUpperCase());
```

can still fail at runtime because the actual value is still the number `123`.

### Actual runtime conversion

```ts
const value = 123;
const str = String(value);
```

### Interview phrase
> Type assertion is a compile-time instruction; it is not a runtime conversion.

---

## Question 17 — Declaration merging vs intersection

### Question
What is the difference between interface declaration merging and intersection types?

### Interview-ready answer
Declaration merging happens automatically when multiple declarations use the same interface name; TypeScript combines them into one interface. Intersection types explicitly combine two or more separate types using `&`.

### Declaration merging

```ts
interface User {
  name: string;
}

interface User {
  age: number;
}
```

The resulting `User` contains both:

```ts
interface User {
  name: string;
  age: number;
}
```

### Intersection

```ts
type A = {
  name: string;
};

type B = {
  age: number;
};

type C = A & B;
```

`A` and `B` remain separate, while `C` contains both properties.

### Key difference
- Declaration merging → same interface name is combined automatically.
- Intersection → separate types are explicitly combined with `&`.

---

## Question 18 — Structural typing

### Question
What is structural typing in TypeScript?

### Interview-ready answer
TypeScript uses structural typing, which means type compatibility is based on the shape of a value rather than the declared name of the type. If an object contains all the required properties, it can be assigned to the target type.

### Example

```ts
interface User {
  name: string;
}

const person = {
  name: "Mayur",
  age: 25
};

const user: User = person; // Allowed
```

`person` has the required `name`, so it is structurally compatible.

### Excess property checking

This is different:

```ts
const user: User = {
  name: "Mayur",
  age: 25
};
```

This can produce an excess property error because the object literal is being directly checked against `User`.

### Interview phrase
> Structural typing means TypeScript cares about shape and compatibility rather than explicit nominal identity.

---

## Question 19 — `null`, `undefined`, and optional properties

### Question
What is the difference between `null`, `undefined`, and `?`?

### Interview-ready answer
An optional property using `?` may be absent. `undefined` represents an undefined value. `null` is an explicit value used to represent the absence of a value.

### Example

```ts
interface User {
  name?: string;
  email: string | null;
}
```

`name` may be absent:

```ts
const user1: User = {
  email: "a@example.com"
};
```

`email` must exist, but may explicitly be `null`:

```ts
const user2: User = {
  email: null
};
```

### Key distinction
- `name?: string` → property may not exist.
- `string | undefined` → property/value may be `undefined`.
- `string | null` → property/value may explicitly be `null`.

---

## Question 20 — `keyof`, `typeof`, and `in`

### Question
What is the difference between `keyof`, `typeof`, and `in`?

### Interview-ready answer
`keyof` produces a union of property names from a type. `typeof` can be used at runtime to inspect a value's primitive type, and in a type position it can derive a type from an existing variable. `in` checks whether a property exists on an object and can be used for narrowing.

### `keyof`

```ts
interface User {
  name: string;
  age: number;
}

type UserKeys = keyof User;
// "name" | "age"
```

### Runtime `typeof`

```ts
if (typeof value === "string") {
  // value is string
}
```

### Type-level `typeof`

```ts
const user = {
  name: "Mayur",
  age: 25
};

type User = typeof user;
```

### `in`

```ts
type User = {
  name: string;
};

type Admin = {
  role: string;
};

function test(value: User | Admin) {
  if ("role" in value) {
    value.role;
  } else {
    value.name;
  }
}
```

### Memory hook
- `keyof` → keys of a type
- `typeof` → runtime type check or derive a type from a value
- `in` → property existence check / narrowing

---

# Question 21 — `Record`, `Map`, and objects

### Question
What is the difference between `Record<K, T>`, `Map`, and a normal JavaScript object? What does this mean?

```ts
type UserRoles = Record<string, string>;
```

### Interview-ready answer
`Record<K, T>` is a TypeScript utility type that describes an object whose keys are `K` and whose values are `T`. A normal object is a runtime JavaScript value. `Map` is a JavaScript collection designed for key-value storage with methods such as `set`, `get`, `has`, and `delete`.

`Record` is mainly about **static type modeling**; it does not create a new runtime data structure.

### Example

```ts
type UserRoles = Record<string, string>;

const roles: UserRoles = {
  mayur: "admin",
  rahul: "user"
};
```

The keys are strings and the values must also be strings.

### When `Record` is useful in React

For a dictionary-like lookup:

```ts
type UserStatus = "online" | "offline" | "away";

const statusLabels: Record<UserStatus, string> = {
  online: "Online",
  offline: "Offline",
  away: "Away"
};
```

This is useful when rendering labels, permissions, configuration, lookup tables, or UI mappings.

### `Map` vs object

Use `Map` when you need runtime collection behavior such as:
- arbitrary key types
- frequent additions/deletions
- `.get()`, `.set()`, `.has()`
- clear collection semantics

Use `Record` when you want to describe the **shape of a key-value object** at compile time.

---

## Question 22 — `Record` with constrained keys

```ts
type Role = "admin" | "user" | "manager";

type Permissions = Record<Role, boolean>;
```

What does this type require? What happens if the `manager` key is missing?

---

## Question 23 — `Readonly<T>`

What is the difference between `Readonly<T>` and `readonly` on a single property?

Give an example of transforming an existing interface into a completely readonly type.

---

## Question 24 — `ReturnType<T>`

What does `ReturnType` do?

```ts
function getUser() {
  return {
    id: 1,
    name: "Mayur"
  };
}

type User = ReturnType<typeof getUser>;
```

What is the type of `User` and why?

---

## Question 25 — `Parameters<T>`

What does this produce?

```ts
function createUser(name: string, age: number) {
  return { name, age };
}

type Params = Parameters<typeof createUser>;
```

Why can this utility type be useful in real applications?

---

## Question 26 — Indexed access types

What does this mean?

```ts
type User = {
  name: string;
  age: number;
};

type Name = User["name"];
```

What is `Name`?

And what does this mean?

```ts
type UserValues = User[keyof User];
```

---

## Question 27 — Generic `keyof` constraint

Explain this function:

```ts
function getProperty<T, K extends keyof T>(obj: T, key: K) {
  return obj[key];
}
```

Why is this safer than:

```ts
function getProperty(obj: any, key: string) {
  return obj[key];
}
```

---

## Question 28 — `extends` in generics vs conditional types

What does this mean?

```ts
T extends string ? "yes" : "no"
```

How is `extends` being used here differently from:

```ts
interface Admin extends User {}
```

---

## Question 29 — Conditional types

What are conditional types in TypeScript?

Explain:

```ts
type IsString<T> = T extends string ? true : false;
```

What are these?

```ts
type A = IsString<string>;
type B = IsString<number>;
```

---

## Question 30 — `infer`

What does `infer` do in conditional types?

Explain:

```ts
type ArrayElement<T> = T extends (infer U)[] ? U : never;
```

What is the result for:

```ts
type A = ArrayElement<string[]>;
type B = ArrayElement<number[]>;
```

---

## Question 31 — Mapped types

What are mapped types?

Explain:

```ts
type Optional<T> = {
  [K in keyof T]?: T[K];
};
```

How is this related to `Partial<T>`?

---

## Question 32 — Template literal types

What are template literal types?

What is the result of:

```ts
type EventName = `on${"Click" | "Change"}`;
```

---

## Question 33 — `satisfies`

What problem does the `satisfies` operator solve?

Compare:

```ts
const config = {
  mode: "dark"
} satisfies { mode: "dark" | "light" };
```

with a normal type annotation and with `as`.

---

## Question 34 — Enums vs union literals

What are the differences between:

```ts
enum Status {
  Loading,
  Success,
  Error
}
```

and:

```ts
type Status = "loading" | "success" | "error";
```

Which would you prefer in a modern TypeScript/React codebase and why?

---

## Question 35 — `unknown` with API responses

Suppose an API response is:

```ts
const data: unknown = await response.json();
```

How would you safely validate and narrow `data` before using it as a `User` object?

Explain why simply doing:

```ts
const user = data as User;
```

is not enough.

---

## Question 36 — Type guards

What is a custom type guard?

Explain:

```ts
function isUser(value: unknown): value is User {
  // ...
}
```

What does `value is User` mean?

---

## Question 37 — `this` typing

How can TypeScript type the `this` parameter inside a function?

Why is this useful?

---

## Question 38 — `never` and exhaustive checking

Why is `never` useful in a switch statement over a discriminated union?

Write an exhaustive checking example.

---

## Question 39 — Function variance / callback typing

Why can function parameter types behave differently when assigning one function to another?

Explain this with a callback example.

---

## Question 40 — React + TypeScript practical question

How would you type a React component that accepts:

- a `title` string
- an optional `count`
- an `onClick` callback
- `children`

Show the props type and component signature.

---

# High-Priority Topics To Master Before a TypeScript Interview

Based on the gaps exposed in this practice, the most important areas are:

1. Generics and generic constraints
2. Type narrowing and custom type guards
3. Utility types
4. Discriminated unions
5. Function overloads
6. Structural typing and excess property checking
7. `keyof` / indexed access / generic property access
8. Conditional types and `infer`
9. Mapped types
10. `as`, `as const`, `satisfies`
11. `never`, exhaustive checking
12. React + TypeScript patterns

