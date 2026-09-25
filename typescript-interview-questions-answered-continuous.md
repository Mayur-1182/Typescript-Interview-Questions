# TypeScript Interview Questions and Interview-Ready Answers

> Based on the uploaded question list. All questions are preserved, including repeated concepts across channels.

### 1. What is TypeScript?

TypeScript is a statically typed superset of JavaScript developed by Microsoft. It adds features such as type annotations, interfaces, generics, enums, and advanced type system capabilities. TypeScript code is compiled or transformed into JavaScript so it can run in JavaScript environments.

### 2. What are Types in TypeScript?

Types describe what kind of value a variable, parameter, property, or function can hold. TypeScript provides primitive types such as `string`, `number`, `boolean`, `bigint`, and `symbol`, along with special types such as `any`, `unknown`, `never`, and `void`. It also supports custom types using interfaces, type aliases, unions, intersections, tuples, enums, and generics.

### 3. What is Static Typing?

Static typing means types are checked during development or compilation instead of waiting until runtime. TypeScript can detect many incorrect assignments, invalid property accesses, and incorrect function arguments before the code runs. This improves maintainability and reduces a class of runtime errors.

### 4. What is the difference between JavaScript and TypeScript?

JavaScript is dynamically typed, while TypeScript adds static type checking on top of JavaScript. TypeScript also provides features such as interfaces, generics, enums, access modifiers, and advanced type manipulation. TypeScript must be transformed into JavaScript before normal JavaScript runtimes execute it.

### 5. What is the difference between `any` and `unknown` types in TypeScript?

Both can hold values of any type, but `unknown` is safer. A value of type `unknown` cannot be used as a specific type until it has been narrowed or checked, while `any` disables type checking for that value. I use `unknown` when the actual type is not known yet and `any` only when I intentionally need to opt out of type safety.

### 6. What is an Interface in TypeScript?

An interface defines the expected shape of an object, class, or function. It is mainly used for describing contracts between different parts of an application. Interfaces can be extended and can participate in declaration merging.

### 7. What is the difference between an Interface (`interface`) and a Type alias (`type`)?

Both can describe object shapes, but they have different strengths. Interfaces support declaration merging and are commonly used for object-oriented contracts, while type aliases are more flexible because they can represent unions, intersections, tuples, primitive aliases, and other type expressions. In practice, I choose based on the required type structure and project conventions.
ś
Both interface and type are used to define the structure of data in TypeScript. The main difference is that interfaces are mainly used for defining object shapes and they support declaration merging, while type aliases can define not only objects but also unions, intersections, primitives, tuples, and other complex types

### 8. What are Union (`|`) and Intersection (`&`) types, and how do they differ?

A union type means a value can be one of several possible types, such as `string | number`. An intersection type combines multiple types, so the resulting value must satisfy all of them, such as `User & Admin`. In simple terms, union means "one of these," while intersection means "all of these."

### 9. What are Enums in TypeScript?

Enums define a named set of constants. TypeScript supports numeric and string enums and also generates runtime JavaScript for regular enums. For many modern applications, string literal unions are often preferred when I only need compile-time type safety without an enum runtime object.
Enums in TypeScript are used to define a set of named constant values. They make code more readable and useful when a variable should have one value from a fixed set of options. For example, we can use an enum for values like Pending, Success, and Failed.”

### 10. What are Generics in TypeScript?

Generics allow me to write reusable code while preserving type information. Instead of hard-coding one type, I define a type parameter such as `T` and let the caller provide the actual type. They are commonly used in reusable functions, APIs, collections, hooks, and utility types.

### 11. What is the `never` type in TypeScript?

`never` represents a value that never occurs. It is commonly used for functions that always throw an error or never finish, and for exhaustive checks where all possible union members have already been handled. It is different from `void`, because `void` means a function returns no useful value, while `never` means execution never reaches a normal return.

### 12. What is the `readonly` modifier in TypeScript?

`readonly` prevents a property from being reassigned through that property after initialization. It is a compile-time restriction and does not automatically make nested objects deeply immutable. It is useful when a value should be treated as immutable by the TypeScript type system.

### 13. Why should you use TypeScript with React / Next.js?

TypeScript improves type safety for component props, state, hooks, event handlers, API responses, and shared models. In React and Next.js projects, it makes large codebases easier to refactor because many incorrect usages are detected by the compiler and editor before runtime. It is especially useful when frontend and backend share domain types.

### 14. What is a generic function in TypeScript and can you write one?

A generic function uses a type parameter so the function can work with different types while preserving the relationship between its inputs and outputs.

```ts
function identity<T>(value: T): T {
  return value;
}
```

Here, `T` is inferred from the argument, so `identity("hello")` returns `string` and `identity(10)` returns `number`.

### 15. What is `as const` in TypeScript and what is the difference with a normal `const`?

`as const` tells TypeScript to infer the most specific literal types and make object properties and array elements readonly. A normal `const` prevents reassignment of the variable itself, but the value can still have wider types and mutable properties.

```ts
const a = "admin"; // type: string
const b = "admin" as const; // type: "admin"
```

### 16. What does the `private` access modifier do when added to a class variable or method?

`private` restricts access to that member from outside the class. It can be accessed only from within the class that declares it. TypeScript also has ECMAScript `#private` fields, which provide runtime-enforced private fields, whereas TypeScript's `private` keyword is primarily a type-system access restriction.

### 17. What is a decorator in TypeScript and what would be a use case?

A decorator is special syntax that can attach behavior or metadata to class-related declarations such as classes and methods. Modern TypeScript supports the standard ECMAScript decorators model, while older TypeScript also has a legacy `experimentalDecorators` implementation. A practical use case is framework-level behavior such as registering classes, wrapping methods, or adding cross-cutting behavior.

### 18. What is the difference between `type` and `interface` in TypeScript?

Both can define object contracts, but `interface` is extendable with `extends` and supports declaration merging. `type` is more flexible for unions, intersections, tuples, mapped types, and other type expressions. For object-oriented contracts I often use interfaces; for complex type composition I often use type aliases.

### 19. What is a type guard in TypeScript?

A type guard is a runtime check that gives TypeScript enough information to narrow a value to a more specific type. Common forms include `typeof`, `instanceof`, the `in` operator, equality checks, and user-defined functions returning a type predicate such as `value is User`.

### 20. How is structural typing different than nominal typing and which one does TypeScript implement?

Structural typing checks compatibility based on the shape of a type rather than its declared name. Nominal typing requires explicit identity or relationships between types. TypeScript primarily uses structural typing, which means two separately declared object types can be compatible if their required members are compatible.

### 21. What is TypeScript?

TypeScript is a statically typed superset of JavaScript. It adds compile-time type checking and features such as interfaces, generics, enums, access modifiers, and advanced type system features, and ultimately produces JavaScript that can run in standard JavaScript environments.

### 22. Explain the features of TypeScript.

Important TypeScript features include static type checking, type inference, interfaces, type aliases, unions and intersections, generics, enums, classes, access modifiers, utility types, type narrowing, decorators, declaration files, and strong editor tooling. These features help make large JavaScript codebases safer and easier to maintain.

### 23. What are `export` and `import` keywords in TypeScript?

`export` makes declarations available outside a module, and `import` brings exported declarations into another module. TypeScript uses the standard JavaScript module system while adding type-only imports and exports such as `import type`.

```ts
export interface User {
  id: number;
}

import type { User } from "./types";
```

### 24. Can TypeScript be used for the backend?

Yes. TypeScript can be used for backend development with environments and frameworks such as Node.js, Express, NestJS, and others. The backend source is still transformed into JavaScript, but TypeScript provides static checking during development.

### 25. How to declare a variable in TypeScript?

Variables can be declared with `let`, `const`, or `var`, just like JavaScript, and TypeScript allows optional type annotations.

```ts
let age: number = 25;
const name: string = "John";
```

Usually I prefer `const` by default and let TypeScript infer the type when the inference is clear.

### 26. List the applications of TypeScript.

TypeScript is used for frontend applications with React, Angular, Vue and similar frameworks, backend applications with Node.js, full-stack applications, libraries, SDKs, command-line tools, and large enterprise applications. It is useful anywhere JavaScript is used, especially when codebases benefit from stronger type safety.

### 27. How can a base constructor be called from a child class?

Use the `super()` call inside the child class constructor. It invokes the parent constructor and passes the required arguments to it.

```ts
class Animal {
  constructor(public name: string) {}
}

class Dog extends Animal {
  constructor(name: string) {
    super(name);
  }
}
```

### 28. What are getters and setters in TypeScript?

Getters allow a property-like way to read a value, while setters allow controlled assignment. They are useful when I need validation, transformation, or encapsulation around a property.

```ts
class User {
  private _name = "";

  get name() {
    return this._name;
  }

  set name(value: string) {
    this._name = value.trim();
  }
}
```

### 29. What is the purpose of `tsconfig.json` file?

`tsconfig.json` defines how TypeScript should compile and type-check a project. It can configure options such as `target`, `module`, `strict`, `jsx`, `outDir`, `rootDir`, path settings, included files, and excluded files. It provides consistent compiler behavior across the project.

### 30. List the advantages of TypeScript.

The main advantages are early error detection, better editor autocomplete, safer refactoring, clearer contracts, improved maintainability, better documentation through types, and support for large codebases. It can reduce many classes of bugs before runtime.

### 31. What are rest parameters in TypeScript?

Rest parameters collect any number of function arguments into an array.

```ts
function sum(...numbers: number[]): number {
  return numbers.reduce((a, b) => a + b, 0);
}
```

The `...` syntax means the function can receive multiple arguments, while TypeScript specifies the element type of the resulting array.

### 32. How to compile TypeScript with Visual Studio Code?

Install TypeScript in the project, create a `tsconfig.json`, and use the TypeScript compiler with `tsc`. For example, `npx tsc` checks and emits files according to the configured project. VS Code also provides TypeScript language support for editing, diagnostics, autocomplete, and navigation.

### 33. List access modifiers supported by TypeScript.

The traditional TypeScript access modifiers are `public`, `private`, and `protected`. `public` is accessible anywhere, `private` is accessible only within the declaring class, and `protected` is accessible within the class and its subclasses. Members are public by default if no modifier is specified.

### 34. List the disadvantages of TypeScript.

TypeScript adds a compilation and type-checking step, introduces additional syntax and learning overhead, and can require extra work for complex types or third-party libraries with poor type definitions. The types are also erased from normal JavaScript output, so compile-time safety does not automatically provide runtime validation of external data.

### 35. How to debug a TypeScript file?

I first use TypeScript compiler errors and editor diagnostics to catch type problems. For runtime debugging, I use source maps with browser or Node.js developer tools so breakpoints can map back to the original `.ts` files. Logging and debugger breakpoints are useful for runtime behavior.

### 36. How can we convert a string to a number with TypeScript?

TypeScript uses JavaScript's runtime conversion functions, such as `Number()`, `parseInt()`, and `parseFloat()`.

```ts
const a = Number("42");
const b = parseInt("42", 10);
const c = parseFloat("42.5");
```

The type annotation can describe the result, but the actual conversion is performed by JavaScript at runtime.

### 37. Explain type aliases in TypeScript.

A type alias gives a name to a type expression.

```ts
type UserId = string;
type User = {
  id: UserId;
  name: string;
};
```

Type aliases are especially useful when defining unions, intersections, tuples, mapped types, conditional types, or reusable object shapes.

### 38. What are nullable types in TypeScript?

A nullable type explicitly allows `null` or `undefined` as part of a type. With strict null checking enabled, I must include them explicitly when they are valid.

```ts
let name: string | null = null;
```

This makes nullability visible and forces safer handling of missing values.

### 39. What is `in` operator in TypeScript?

The `in` operator checks whether a property exists on an object and can also act as a type guard for union types.

```ts
type Admin = { permissions: string[] };
type User = { name: string };

function print(value: Admin | User) {
  if ("permissions" in value) {
    console.log(value.permissions);
  }
}
```

Here TypeScript narrows the value to `Admin` inside the condition.

### 40. Explain index types in TypeScript.

Index types allow code to work with property names dynamically while still preserving type information. A common pattern is using `keyof` and indexed access types.

```ts
type User = {
  id: number;
  name: string;
};

type UserKey = keyof User; // "id" | "name"
type UserValue = User[UserKey]; // number | string
```

This is useful for generic utilities that operate on object keys and values.

### 41. What are mapped types in TypeScript?

Mapped types create a new type by iterating over the keys of another type and transforming their modifiers or value types.

```ts
type User = {
  name: string;
  age: number;
};

type OptionalUser = {
  [K in keyof User]?: User[K];
};
```

Built-in utility types such as `Partial`, `Readonly`, and `Pick` are based on this idea.

### 42. What is meant by contextual typing?

Contextual typing means TypeScript determines a type from the surrounding context instead of requiring an explicit annotation.

```ts
const numbers = [1, 2, 3];

numbers.map((n) => n * 2);
```

TypeScript knows `n` is a `number` because `map` provides the expected callback type.

### 43. Distinguish between TypeScript and JavaScript.

JavaScript is the runtime language, while TypeScript adds a static type system and developer tooling on top of JavaScript. TypeScript provides compile-time checking and features such as interfaces and generics, while the final runtime execution normally happens as JavaScript.

### 44. What is JSX in TypeScript?

JSX is a syntax extension used to describe UI elements, commonly with React. When JSX is used in a TypeScript file, the file normally uses the `.tsx` extension. TypeScript checks the JSX structure and types while the configured JSX transform produces JavaScript.

### 45. Define static typing.

Static typing means the compiler or type checker verifies type relationships before the program runs. TypeScript uses static analysis to detect many type-related problems during development rather than waiting for runtime.

### 46. What is meant by type inference?

Type inference is TypeScript's ability to determine a type automatically from the code without an explicit annotation.

```ts
const age = 25;
```

TypeScript infers `age` as `number`. Good inference reduces unnecessary type annotations while preserving type safety.

### 47. How to create objects in TypeScript?

Objects are created using normal JavaScript syntax, and TypeScript can describe their shape using annotations, interfaces, or type aliases.

```ts
interface User {
  name: string;
  age: number;
}

const user: User = {
  name: "John",
  age: 25,
};
```

### 48. Explain different data types in TypeScript.

TypeScript supports primitive types such as `string`, `number`, `boolean`, `bigint`, `symbol`, `null`, and `undefined`. It also has special types such as `any`, `unknown`, `never`, and `void`, plus object types, arrays, tuples, functions, enums, unions, intersections, literal types, and custom types through interfaces and type aliases.

### 49. What are the benefits of using TypeScript?

TypeScript gives early feedback about incorrect types, better autocomplete and navigation, safer refactoring, clearer APIs, and better maintainability for large applications. It is particularly useful when multiple developers work on the same codebase.

### 50. How to install TypeScript?

For a project, I usually install it as a development dependency:

```bash
npm install -D typescript
```

Then I can initialize configuration with `npx tsc --init` and run the compiler with `npx tsc`.

### 51. What are decorators in TypeScript?

Decorators provide syntax for adding behavior or metadata around class-related declarations. Modern TypeScript supports standard ECMAScript decorators, while TypeScript also has legacy decorator support controlled by `experimentalDecorators`. The exact API and semantics depend on which decorator model the project uses.

### 52. What are mixins in TypeScript?

Mixins are a pattern for composing behavior from multiple class-like sources into a class. They are useful when I want to reuse capabilities without forcing a single inheritance chain. TypeScript can type mixins using generic constructor types.

### 53. Explain classes in TypeScript.

TypeScript classes extend JavaScript classes with type annotations and features such as access modifiers, parameter properties, abstract classes, readonly members, and typed constructors and methods. They support encapsulation and object-oriented patterns while still compiling to JavaScript classes or compatible output depending on the target.

### 54. What is a namespace and how to declare it?

A namespace is a TypeScript-specific way to group related declarations under a named scope. It is declared using the `namespace` keyword.

```ts
namespace Utils {
  export function add(a: number, b: number) {
    return a + b;
  }
}
```

For modern applications, ES modules are generally preferred for organizing application code, while namespaces still appear in some older code and declaration files.

### 55. Explain the components of TypeScript.

At a high level, TypeScript consists of the language and type system, the TypeScript compiler, and the language service/tooling used by editors. The compiler performs type checking and emits JavaScript or declaration files, while the language service powers features such as autocomplete, navigation, and diagnostics.

### 56. What are the recent advancements in TypeScript?

For a current interview answer, I would mention recent compiler and type-system improvements rather than listing every release. TypeScript 6.0 introduces changes such as stricter defaults, more modern module behavior, and deprecations preparing for the TypeScript 7 transition. TypeScript 5.9 added features such as `import defer`, a stable `node20` module mode, and compiler/editor improvements. The important point is that recent TypeScript releases continue moving toward stricter typing, modern JavaScript modules, and better compiler performance.

### 57. Describe `as` syntax in TypeScript.

`as` performs a type assertion, telling TypeScript to treat a value as a specific type. It does not perform a runtime conversion or validation.

```ts
const value = document.getElementById("app") as HTMLDivElement;
```

The assertion only affects compile-time type checking.

### 58. Define lambda function in TypeScript.

In TypeScript, the term lambda function usually refers to an arrow function.

```ts
const add = (a: number, b: number): number => a + b;
```

Arrow functions provide concise function syntax and have lexical `this` behavior.

### 59. What are conditional types in TypeScript?

Conditional types choose one type or another based on a type relationship.

```ts
type Message<T> = T extends string ? "text" : "other";
```

They follow the pattern `T extends U ? X : Y` and are heavily used in advanced generic utilities.

### 60. What is an interface with reference to TypeScript?

An interface is a named contract that describes the shape of values, especially objects and classes. It defines what members should exist and their types without providing normal runtime implementation.

```ts
interface Product {
  id: number;
  name: string;
}
```

### 61. What is a `declare` keyword in TypeScript?

`declare` tells TypeScript that something exists at runtime but is defined outside the current TypeScript code being emitted. It is commonly used in declaration files and ambient declarations.

```ts
declare const API_URL: string;
```

No JavaScript is emitted for the declaration itself.

### 62. What are object-oriented principles supported by TypeScript?

TypeScript supports the main OOP principles: encapsulation, inheritance, abstraction, and polymorphism. These are implemented using classes, access modifiers, abstract classes, interfaces, method overriding, and related language features.

### 63. Explain index signatures in TypeScript.

An index signature describes objects whose property names are dynamic but whose property values follow a known type.

```ts
interface Scores {
  [key: string]: number;
}

const scores: Scores = {
  math: 90,
  science: 85,
};
```

It is useful when the exact keys are not known ahead of time.

### 64. What are assert signatures?

Assert signatures describe functions that either establish a condition or throw an error. They use the `asserts` keyword and allow TypeScript to narrow types after the function returns successfully.

```ts
function assertString(value: unknown): asserts value is string {
  if (typeof value !== "string") {
    throw new Error("Expected string");
  }
}
```

### 65. What is type assertion? Explain its types.

Type assertion tells TypeScript to treat a value as a particular type without performing runtime checking. The two common syntaxes are `value as Type` and angle-bracket syntax `<Type>value`.

```ts
const value = input as string;
const value2 = <string>input;
```

The angle-bracket syntax is not suitable inside JSX/TSX, so `as` is generally preferred in React code.

### 66. Explain how TypeScript files can be supported from node_modules.

TypeScript can obtain type information for JavaScript packages from declaration files. Packages can ship their own `.d.ts` files and expose them through fields such as `types` or `typings` in `package.json`; otherwise community definitions are often provided through packages under `@types`.

For example:

```bash
npm install -D @types/node
```

This allows TypeScript to understand Node.js APIs during type checking.

### 67. Explain TypeScript generics.

Generics let me create reusable code that works with multiple types while preserving those types.

```ts
function first<T>(items: T[]): T | undefined {
  return items[0];
}
```

The type parameter `T` keeps the input and output relationship intact.

### 68. What are recursive type aliases?

A recursive type alias refers to itself, directly or indirectly. It is useful for recursive data structures such as trees, linked lists, and nested JSON-like structures.

```ts
type TreeNode = {
  value: string;
  children: TreeNode[];
};
```

### 69. Explain tail recursion elimination on conditional types.

TypeScript can optimize certain recursive conditional type computations when the recursive call is in a tail position. This allows some deeply recursive type definitions to be evaluated with less risk of excessive type-instantiation depth and better compiler performance. It is primarily a compiler optimization for advanced type-level programming, not runtime recursion.

### 70. Explain the `Awaited` type and promise improvements.

`Awaited<T>` models what happens when a value is passed through `await`, including recursively unwrapping promise-like types.

```ts
type A = Awaited<Promise<string>>; // string
type B = Awaited<Promise<Promise<number>>>; // number
```

It is useful when deriving the resolved type of asynchronous operations. TypeScript also uses `Awaited` in relevant promise-related type definitions, such as improving the typing of `Promise.resolve`.

### 71. How do you combine string literal types in TypeScript (template string types)?

Template literal types create new string literal types by combining other literal types.

```ts
type Role = "admin" | "user";
type Permission = `${Role}_read` | `${Role}_write`;
```

They are useful for strongly typed event names, routes, keys, IDs, and other string patterns.

### 72. What is a TypeScript generic and why would you use one?

A generic is a type parameter that lets code work with multiple types while preserving type relationships. I use generics to avoid duplicating similar code and to keep reusable functions, classes, components, and utilities type-safe.

### 73. How do you write a conditional type in TypeScript?

A conditional type uses the syntax `T extends U ? X : Y`.

```ts
type IsString<T> = T extends string ? true : false;
```

It chooses a type based on whether one type is assignable to another.

### 74. How would you generate a TypeScript type for the return value of an asynchronous function without manually typing it?

I can use `Awaited` together with `ReturnType`.

```ts
async function getUser() {
  return { id: 1, name: "John" };
}

type User = Awaited<ReturnType<typeof getUser>>;
```

`ReturnType` gets the function's return type, and `Awaited` unwraps the promise to get the resolved value type.

### 75. How do `.d.ts` declaration files work in TypeScript?

A `.d.ts` file contains declarations used for type checking but normally does not emit JavaScript. It describes the types and APIs of code that exists elsewhere, such as a JavaScript library or a global runtime object. They are heavily used by libraries to provide TypeScript support.

### 76. Name one difference between a type and an interface in TypeScript.

One key difference is that interfaces support declaration merging, while type aliases do not merge in the same way.

```ts
interface User {
  name: string;
}

interface User {
  age: number;
}
```

The resulting `User` interface contains both properties.

### 77. What is a triple-slash directive (`/// <reference ... />`) and why would you use them?

A triple-slash directive is a special single-line TypeScript directive used to provide compiler instructions, such as referencing declarations or controlling certain compilation behavior. Historically, `/// <reference path="..." />` was used to link declaration files. In modern module-based projects, normal `import` statements are generally preferred for module dependencies.

### 78. What is a TypeScript `Record` utility type and what is it used for?

`Record<Keys, Type>` creates an object type whose specified keys all map to the same value type.

```ts
type Roles = "admin" | "user";

type RoleLabels = Record<Roles, string>;
```

It is useful when the set of keys is known and every key should have a value of a consistent type.

### 79. What is the difference between JavaScript and TypeScript?

JavaScript is dynamically typed and executed by JavaScript runtimes. TypeScript adds static type checking and additional language features while remaining compatible with JavaScript. TypeScript source is transformed into JavaScript before normal runtime execution.

### 80. Does TypeScript improve our code when we just change the extension of the file from `.js` to `.ts`?

No. Simply renaming a file does not automatically add meaningful type safety. TypeScript can infer some types from existing JavaScript code, but the real benefits come from type checking, appropriate compiler settings, type annotations where needed, and actually resolving type errors.

### 81. How to define basic types inside TypeScript?

Basic types are declared using type annotations or inferred automatically.

```ts
let name: string = "John";
let age: number = 25;
let active: boolean = true;
```

TypeScript also supports arrays, tuples, objects, functions, unions, literals, and many advanced types.

### 82. What is the difference between explicit and implicit types inside TypeScript?

An explicit type is written by the developer.

```ts
let age: number = 25;
```

An implicit type is inferred by TypeScript from the value or context.

```ts
let age = 25;
```

Both can be type-safe; the choice depends on whether the explicit annotation improves clarity or is needed to define a broader or specific contract.

### 83. How to type functions and function return types in TypeScript?

I can type parameters and the return type directly in the function signature.

```ts
function add(a: number, b: number): number {
  return a + b;
}
```

TypeScript can often infer the return type, but explicit return types are useful for public APIs and when I want to document or constrain the contract.

### 84. What is an interface inside TypeScript?

An interface defines the required shape of a value, usually an object or class contract.

```ts
interface User {
  id: number;
  name: string;
}
```

It improves consistency and makes object-oriented contracts easier to understand and reuse.

### 85. What is a type (`type` alias) inside TypeScript?

A type alias assigns a name to any valid TypeScript type expression.

```ts
type UserId = string;

type User = {
  id: UserId;
  name: string;
};
```

Unlike interfaces, type aliases can directly represent unions, intersections, tuples, conditional types, and other composed types.

### 86. What is the difference between a type and an interface?

Interfaces are primarily designed for describing object contracts and support declaration merging and `extends`. Type aliases can describe object types too, but they also naturally support unions, intersections, tuples, primitives, mapped types, and conditional types. Neither is universally better; the right choice depends on the use case.

### 87. Do you know what is Union (`|`) inside TypeScript?

A union means a value can be one of several possible types.

```ts
let id: string | number;
```

Before using type-specific members, TypeScript may require me to narrow the union to a specific type.

### 88. What do you know about type narrowing inside TypeScript?

Type narrowing is the process of reducing a broad type to a more specific type based on runtime checks. Common narrowing techniques include `typeof`, `instanceof`, `in`, equality checks, truthiness checks, discriminated unions, and user-defined type guards.

---

# Quick Interview Revision Sheet

## High-priority topics from this list

For a React/Next.js developer interview, make sure you can explain these without memorizing definitions word-for-word:

1. TypeScript vs JavaScript
2. Static typing and type inference
3. `any` vs `unknown`
4. `interface` vs `type`
5. Union vs intersection
6. Generics
7. Type guards and narrowing
8. `never`, `void`, `unknown`
9. `as const`
10. Type assertion
11. `keyof` and indexed access types
12. Mapped types
13. Conditional types
14. `Record`
15. `Awaited` and `ReturnType`
16. `readonly`
17. Access modifiers
18. Classes, inheritance, `super()`, getters and setters
19. `.d.ts` declaration files
20. `declare`
21. `tsconfig.json`
22. Modules with `import` and `export`
23. Decorators
24. Namespaces vs modules
25. Template literal types
26. Recent TypeScript compiler changes

## Interview rule

Do not answer TypeScript questions by only giving definitions. A stronger answer is usually:

**Definition → why it is used → one short example → one important limitation or distinction.**

Example:

**Question:** What is `unknown`?

**Answer:** `unknown` is a type-safe way to represent a value whose type is not known yet. Unlike `any`, I cannot directly use the value as a specific type until I narrow it. I prefer `unknown` for data coming from external or untrusted sources because it forces me to validate the value before using it.

---

# Sources and Current-Version Notes

The question set itself comes from the uploaded file.

For current TypeScript behavior, the answers involving recent releases, decorators, `Awaited`, namespaces/modules, and declaration files should be understood in the context of current TypeScript documentation.

As of the current documentation checked for this revision:

- TypeScript 6.0 introduces several modern-configuration and stricter-default changes as part of the transition toward TypeScript 7.
- TypeScript 5.9 introduced `import defer`, a stable `node20` module mode, and other compiler/editor improvements.
- `Awaited` is the utility type used to model recursive promise unwrapping.
- Modern ECMAScript decorators are supported in TypeScript, while the older `experimentalDecorators` option refers to the legacy decorator implementation.
- TypeScript documentation recommends ES modules over namespaces for new application code.
