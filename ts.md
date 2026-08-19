# TypeScript Interview Questions & Answers (260+)

## Section 1: Basic Types & Type Annotations

**1. What is type annotation in TypeScript?**
It's explicitly telling TypeScript what type a variable, parameter, or return value should be, using a colon syntax like `let age: number`.

**2. What happens if you don't provide a type annotation?**
TypeScript uses type inference — it looks at the assigned value and automatically figures out the type on its own.

**3. Can you change a variable's type after declaration?**
No. Once a type is set (explicit or inferred), TypeScript locks it and throws an error if you assign a different type later.

**4. What is the `number` type in TypeScript?**
It represents all numbers — integers, floats, and special values like `Infinity` and `NaN`. There's no separate int/float type.

**5. What is the difference between `string` and `String`?**
`string` (lowercase) is the primitive type you should always use. `String` (uppercase) is the object wrapper and should be avoided.

**6. What is the `symbol` type?**
A unique, immutable primitive value, often used as a special object property key so it never collides with other keys.

**7. What is the `bigint` type?**
Used to represent whole numbers larger than what `number` can safely handle, written with an `n` suffix like `100n`.

**8. How do you declare an array type?**
Two ways: `number[]` or `Array<number>`. Both mean the same thing — an array containing only numbers.

**9. What is a tuple type?**
A fixed-length array where each position has a specific, known type, e.g. `[string, number]` for a name and age pair.

**10. Can tuple length be enforced strictly?**
Yes, TypeScript checks both the number of elements and their exact types/order — adding extra elements causes an error.

**11. What is the `void` type used for?**
It's used as a return type for functions that don't return any value, like a function that just logs something.

**12. What is the `null` type?**
Represents an intentional "no value" — a deliberate absence, as opposed to a variable that was never assigned.

**13. What is the `undefined` type?**
Represents a variable that has been declared but not yet assigned a value, or a missing object property.

**14. What is `strictNullChecks`?**
A compiler flag that treats `null` and `undefined` as distinct types, so you can't assign them to a variable unless explicitly allowed.

**15. What is object type annotation?**
Describing the shape of an object inline, like `{ name: string; age: number }`, without creating a separate interface.

**16. How do you type a function variable?**
By specifying its parameter types and return type, e.g. `let add: (a: number, b: number) => number`.

**17. What is type widening?**
When TypeScript infers a broader type than the literal value assigned, e.g. `let x = "hi"` gets type `string`, not `"hi"`.

**18. What is const assertion?**
Using `as const` to lock a value to its most specific literal type instead of letting TypeScript widen it.

**19. Can you have mixed type arrays?**
Yes, using a union type like `(string | number)[]`, which allows both strings and numbers in the same array.

**20. What is the difference between `Array<number>` and `number[]`?**
None functionally — they're two syntaxes for the exact same array type; `number[]` is just more common.

---

## Section 2: Type System Fundamentals

**21. What is type inference?**
TypeScript's ability to automatically determine a variable's type from its initial value without you writing an annotation.

**22. What is union type syntax?**
Using `|` to say a value can be one of several types, e.g. `string | number` means it can be either.

**23. What is intersection type syntax?**
Using `&` to combine multiple types into one, so the result must satisfy all of them at once.

**24. What is a type alias?**
A custom name given to any type using the `type` keyword, useful for reusing complex types easily.

**25. Can type aliases be recursive?**
Yes, a type can reference itself, which is useful for tree-like or nested structures such as JSON values.

**26. What is nominal typing?**
A type system where compatibility is based on explicit names/declarations — TypeScript does NOT use this by default.

**27. What is structural typing?**
TypeScript's actual approach — two types are compatible if their shapes match, regardless of their names.

**28. What is excess property checking?**
TypeScript flags an error if you pass an object literal with extra properties not defined in the target type.

**29. What are literal types?**
Types that represent one exact value, like `"left"` or `1`, instead of the broader `string` or `number` type.

**30. What is type assertion?**
Telling the compiler "trust me, treat this value as this type" using `as`, without changing the value at runtime.

**31. What are the two type assertion syntaxes?**
The `as Type` syntax, and the older angle-bracket `<Type>value` syntax (which conflicts with JSX so is rarely used).

**32. What is double assertion?**
Asserting a value to `unknown` first and then to the target type — used to bypass normal assertion safety checks.

**33. What is the `satisfies` operator?**
Checks that a value matches a given type while still keeping the value's own narrower inferred type intact.

**34. What is index signature?**
A way to type objects with dynamic/unknown keys, e.g. `{ [key: string]: number }` for any string key holding a number.

**35. Can you mix index signatures with fixed properties?**
Yes, as long as the fixed properties' types are compatible with the index signature's value type.

**36. What is the `keyof` operator?**
Produces a union of all the property names (keys) of a given type, useful for type-safe key access.

**37. What is the `typeof` operator in types?**
Extracts the type of an existing variable or object so you can reuse it as a type elsewhere.

**38. What is indexed access type?**
Accessing the type of a specific property using bracket syntax, like `Person["age"]` to get that property's type.

**39. What is the difference between `type` and `interface` for objects?**
Interfaces can be extended and merged automatically; type aliases are more flexible for unions and complex compositions.

**40. Can you extend a type alias?**
Not with `extends`, but you can achieve the same result using intersection (`&`) to combine types.

**41. What is declaration merging?**
When you declare the same interface name multiple times, TypeScript automatically combines all their properties into one.

**42. What is the `in` operator in types?**
Used inside mapped types to loop over each key of a type, similar to a for-in loop but at the type level.

**43. What is a mapped type?**
A type that transforms every property of another type, like making all properties optional or readonly.

**44. What is the `-?` modifier?**
Used in mapped types to remove the optional (`?`) modifier, forcing all properties to become required.

**45. What is the `-readonly` modifier?**
Used in mapped types to strip the `readonly` modifier, making previously readonly properties mutable again.

---

## Section 3: Functions

**46. How do you type function parameters?**
Add a colon and type after each parameter name, e.g. `function greet(name: string)`.

**47. How do you type function return values?**
Add a colon and type after the closing parenthesis of the parameter list, e.g. `function add(): number`.

**48. What happens if you don't specify return type?**
TypeScript infers the return type automatically based on what the function actually returns.

**49. How do you type optional parameters?**
Add a `?` after the parameter name, meaning the caller can omit it entirely, e.g. `name?: string`.

**50. What is the difference between optional and undefined parameter?**
Optional (`?`) can be left out entirely; a parameter typed as `T | undefined` must still be passed, even if it's `undefined`.

**51. How do you set default parameter values?**
Assign a value using `=` in the parameter list; TypeScript then infers the type from that default value.

**52. How do you type rest parameters?**
Use an array type after the spread syntax, e.g. `...numbers: number[]` to accept any number of number arguments.

**53. What is function overloading?**
Defining multiple call signatures for the same function name so it behaves differently based on argument types.

**54. How many overload signatures can you have?**
As many as needed — there's no hard limit, but the actual implementation must correctly handle every declared case.

**55. What is the order of overload signatures?**
List the most specific signatures first and the most general one last, since TypeScript checks them top to bottom.

**56. How do you type arrow functions?**
The same way as regular functions — annotate parameter types and optionally the return type.

**57. How do you type a callback function?**
Define the callback's parameter as a function type describing its expected inputs and output, e.g. `(x: number) => void`.

**58. What is contextual typing in functions?**
When TypeScript infers a callback's parameter types automatically based on where it's used, like inside `.forEach()`.

**59. How do you type `this` in a method?**
Add `this` as a fake first parameter with its type, so TypeScript knows what `this` refers to inside the function.

**60. What is a function type expression?**
An inline type describing a function's shape, e.g. `let fn: (a: number) => number`, without naming it separately.

**61. What is a call signature?**
Describing a function type using object-like syntax inside an interface or type, e.g. `{ (x: number): number }`.

**62. What is a construct signature?**
Similar to a call signature but for constructor functions, written with `new`, e.g. `{ new (name: string): Person }`.

**63. How do you create a function that accepts any number of arguments?**
Use rest parameters with an array type, like `(...args: unknown[])`, to safely accept a variable amount of input.

**64. What is parameter destructuring in TypeScript?**
Destructuring an object parameter directly while still typing its shape, e.g. `({ name, age }: { name: string; age: number })`.

**65. Can you type destructured array parameters?**
Yes, by giving the parameter a tuple type, e.g. `([a, b]: [number, number])`.

**66. What is the `never` return type used for?**
For functions that never successfully return, like ones that always throw an error or run forever.

**67. How do you type async functions?**
Their return type is automatically wrapped in `Promise`, so returning a `string` becomes `Promise<string>`.

**68. How do you type generator functions?**
Using `Generator<T>` or `IterableIterator<T>` as the return type, where T is the type of yielded values.

**69. What is the difference between `void` and `undefined` return?**
`void` means the return value is ignored (any or no return is fine); `undefined` means the function must explicitly return `undefined`.

**70. How do you type a function that accepts another function?**
Type the parameter as a function signature, e.g. `fn: (x: number) => number`, describing what that passed-in function must look like.

---

## Section 4: Interfaces

**71. What is an interface?**
A contract that defines the exact shape (properties and methods) an object must have.

**72. How do you make interface properties optional?**
Add a `?` after the property name so the object doesn't have to include it.

**73. How do you make interface properties readonly?**
Add the `readonly` keyword before the property, so it can only be set once (usually at creation).

**74. Can you have both optional and readonly?**
Yes, they can be combined on the same property, e.g. `readonly email?: string`.

**75. How do you extend an interface?**
Use the `extends` keyword to inherit all properties from another interface into a new one.

**76. Can an interface extend multiple interfaces?**
Yes, just separate them with commas, e.g. `interface C extends A, B`.

**77. Can an interface extend a type alias?**
Yes, as long as the type alias represents an object shape (not a union or primitive).

**78. What is interface declaration merging?**
When you declare an interface with the same name more than once, TypeScript merges all versions into a single interface.

**79. How do you define methods in interfaces?**
Either as a method shorthand (`greet(): void`) or as a property holding a function type (`greet: () => void`).

**80. What is the difference between method and property function syntax?**
Method shorthand syntax supports overloads more naturally; property function syntax is stricter about parameter compatibility.

**81. How do you define string index signature?**
Using `[key: string]: Type` to allow any string key to map to a value of that type.

**82. How do you define number index signature?**
Using `[index: number]: Type`, typically used for array-like structures.

**83. Can you have both string and number index signatures?**
Yes, but the number index's value type must be compatible with (a subtype of) the string index's type.

**84. How do you implement an interface in a class?**
Use the `implements` keyword after the class name to force the class to fulfill that interface's contract.

**85. Can a class implement multiple interfaces?**
Yes, list them separated by commas after `implements`, and the class must satisfy all of them.

**86. What happens if you don't implement all interface members?**
TypeScript throws a compile-time error saying the class is missing required properties or methods.

**87. Can interfaces have private properties?**
No, interfaces can only describe public members — they can't define private or protected access.

**88. How do you create a hybrid type (callable + object)?**
Define both a call signature and regular properties/methods inside the same interface.

**89. Can interfaces extend classes?**
Yes, an interface can extend a class, inheriting its member shapes (including private/protected members structurally).

**90. What is the difference between interface and abstract class?**
An interface has zero implementation, just structure; an abstract class can include actual working code alongside abstract methods.

---

## Section 5: Classes

**91. How do you define a class in TypeScript?**
Using the `class` keyword with typed properties, a typed constructor, and typed methods.

**92. What are access modifiers?**
Keywords (`public`, `private`, `protected`) that control where a class member can be accessed from.

**93. What is the default access modifier?**
`public` — if you don't specify a modifier, the member is accessible from anywhere by default.

**94. What does `private` mean?**
The member is only accessible from inside the class itself, not from subclasses or outside code.

**95. What does `protected` mean?**
The member is accessible inside the class and any of its subclasses, but not from outside code.

**96. What is constructor parameter shorthand?**
Adding access modifiers directly to constructor parameters so TypeScript auto-creates and assigns the class properties.

**97. How do you define readonly properties?**
Add `readonly` before the property declaration; it can only be assigned in the constructor or at declaration.

**98. Can you modify readonly properties after construction?**
No, any attempt to reassign a readonly property after the constructor runs will cause a compile error.

**99. How do you define static properties?**
Use the `static` keyword, making the property belong to the class itself rather than individual instances.

**100. How do you access static members inside instance methods?**
Reference them using the class name (e.g. `ClassName.property`), not `this`.

**101. What are getters and setters?**
Special methods (`get`/`set`) that let you control how a property is read or written, often adding validation logic.

**102. Can a getter and setter have different types?**
No, TypeScript requires the getter and setter for the same property to share the same type.

**103. How do you extend a class?**
Use `extends` to inherit all properties and methods from a parent class into a child class.

**104. How do you call parent constructor?**
Call `super(...)` as the very first statement inside the subclass's constructor.

**105. How do you override methods?**
Define a method with the same name in the subclass; it replaces the parent's version when called on that subclass.

**106. How do you call parent method from override?**
Use `super.methodName()` inside the overriding method to still run the parent's original logic.

**107. What is an abstract class?**
A class that can't be instantiated directly — it's meant only to be extended by other classes.

**108. What is an abstract method?**
A method declared in an abstract class with no body; subclasses are forced to provide their own implementation.

**109. Can abstract classes have constructors?**
Yes, and subclasses must call that constructor via `super()` even though the abstract class itself can't be instantiated.

**110. Can you mix abstract and concrete methods?**
Yes, an abstract class can have both fully implemented methods and abstract ones needing implementation.

**111. What is method overloading in classes?**
Declaring multiple signatures for the same class method name, similar to function overloading.

**112. How do you make a class implement an interface?**
Add `implements InterfaceName` after the class declaration, then fulfill every member the interface requires.

**113. Can a class implement multiple interfaces?**
Yes, separate interface names with commas, and the class must satisfy the requirements of all of them.

**114. What is the difference between `implements` and `extends`?**
`extends` inherits actual code/behavior from a parent; `implements` only enforces that a contract's shape is fulfilled.

**115. Can you create private constructors?**
Yes, marking the constructor `private` prevents creating instances from outside — often used for singleton patterns.

---

## Section 6: Generics

**116. What is a generic type parameter?**
A placeholder type (like `T`) that lets a function, class, or interface work with different types while staying type-safe.

**117. How do you call a generic function?**
Either explicitly specify the type (`identity<string>("hi")`) or let TypeScript infer it automatically from the argument.

**118. Can you have multiple type parameters?**
Yes, separate them with commas, e.g. `function pair<T, U>(a: T, b: U)`.

**119. What is a generic constraint?**
Restricting what types can be used for a generic parameter using `extends`, e.g. `T extends { length: number }`.

**120. How do you constrain to a specific type?**
Add `extends TypeName` after the generic parameter to limit which types are acceptable.

**121. How do you use `keyof` in generic constraints?**
Constrain one generic parameter to be a key of another, e.g. `K extends keyof T`, for safe property access.

**122. What is a generic interface?**
An interface that takes type parameters, letting it describe different shapes depending on what type is passed in.

**123. What is a generic class?**
A class that accepts type parameters so its properties/methods can work with different data types safely.

**124. Can generic classes have static members with type parameters?**
No, static members are shared across all instances, so they can't depend on the class's specific type parameter.

**125. What is a generic type alias?**
A `type` declaration that accepts type parameters, e.g. `type Pair<T, U> = { first: T; second: U }`.

**126. What is default type parameter?**
A fallback type used if no type argument is provided when using a generic, e.g. `interface Request<T = string>`.

**127. Can you use type parameters in constraints?**
Yes, one generic parameter can be constrained by another, e.g. `function copy<T extends U, U>(...)`.

**128. What is a generic arrow function?**
An arrow function with a type parameter; in `.tsx` files you add a trailing comma like `<T,>` to avoid JSX confusion.

**129. How do you create a generic factory function?**
Write a function that accepts a constructor type and returns a new instance of it, using generics to preserve the type.

**130. What is variance in generics?**
How type relationships (like subtype compatibility) carry through generic types — for example, arrays are covariant in TypeScript.

**131. What is the `infer` keyword?**
Used inside conditional types to capture and extract a type for reuse, commonly seen in things like `ReturnType`.

**132. How do you infer multiple types?**
Use multiple `infer` keywords within the same conditional type to capture different parts, like function arguments.

**133. What is a recursive generic type?**
A generic type that refers to itself, useful for describing nested or tree-like data structures like JSON.

**134. How do you constrain array elements?**
Constrain the generic to `any[]` or a more specific array shape, e.g. `T extends any[]`.

**135. What is a generic conditional type?**
A type that picks between two results depending on whether a generic parameter satisfies a condition.

**136. How do you distribute conditional types?**
By default, when a union type is passed into a conditional type, TypeScript applies the condition to each member separately.

**137. How do you prevent distribution?**
Wrap the type parameter in a tuple (e.g. `[T] extends [U]`) so the whole union is checked at once instead of splitting.

**138. What are generic utility types?**
Built-in generic helper types (like `Partial<T>`, `Readonly<T>`) that transform other types in common, reusable ways.

**139. How do you create a generic mapped type?**
Combine `keyof` with `in` inside a generic type, iterating over the properties of a type parameter to transform them.

**140. What is a generic higher-order type?**
A generic type that itself takes another generic type as input, similar to higher-order functions but at the type level.

---

## Section 7: Advanced Types

**141. What is a conditional type?**
A type that resolves to one of two types depending on a true/false condition, written like a ternary expression.

**142. What is the ternary syntax in conditional types?**
`T extends U ? X : Y` — if T is assignable to U, the result is X, otherwise it's Y.

**143. What is distributive conditional type?**
When the generic parameter in a conditional type is a union, TypeScript automatically applies the condition to each member.

**144. How do you create non-distributive conditional type?**
Wrap the generic parameter in square brackets so the union is treated as a single unit instead of being split apart.

**145. What is mapped type?**
A type built by looping over another type's keys and transforming each property, like making them optional or readonly.

**146. What is key remapping in mapped types?**
Using `as` inside a mapped type to rename keys during the transformation, e.g. turning `name` into `getName`.

**147. How do you filter properties in mapped types?**
Map a key to `never` conditionally to exclude it from the resulting type based on some condition.

**148. What is template literal type?**
A string type built using template-string-like syntax, combining literal text with other types, e.g. `` `Hello ${string}` ``.

**149. How do you combine template literal types?**
When you use union types inside a template literal, TypeScript generates every possible combination automatically.

**150. What are intrinsic string manipulation types?**
Built-in type helpers (`Uppercase`, `Lowercase`, `Capitalize`, `Uncapitalize`) that transform string literal types.

**151. What is type narrowing?**
The process where TypeScript refines a broader type into a more specific one inside conditional checks, like after `typeof`.

**152. What is control flow analysis?**
TypeScript's tracking of how a variable's type changes as your code executes, based on assignments and checks.

**153. What is type guard?**
A function or expression that checks a value's type at runtime and lets TypeScript narrow it accordingly, e.g. `typeof x === "string"`.

**154. What is assertion function?**
A function that throws an error if a condition isn't met, and tells TypeScript to treat the value as narrowed afterward.

**155. What is discriminated union?**
A union of object types that all share a common literal property (a "tag") used to distinguish which type you're dealing with.

**156. What is exhaustiveness checking?**
Using the `never` type in a default case to make sure every possibility in a union has been handled.

**157. What is branded type?**
A technique of adding a fake unique property to a primitive type to simulate nominal typing and prevent mixing similar types.

**158. What is opaque type?**
Similar to branded types — hiding a type's real structure behind a unique tag so it can't be accidentally substituted.

**159. What is index type query?**
Using `keyof` on a type to retrieve a union of all its property names.

**160. What is indexed access type?**
Accessing a specific property's type from another type using bracket notation, like `Type["propertyName"]`.

**161. What is the `this` type?**
A special type that refers to the current class instance, often used so methods can return `this` for chaining.

**162. What is recursive type alias?**
A type alias that includes itself in its own definition, useful for nested structures like trees or JSON values.

**163. What is tail recursion in types?**
A pattern for writing recursive types so each step builds on an accumulator, helping avoid hitting recursion depth limits.

**164. What is type instantiation depth limit?**
TypeScript caps how deeply recursive types can expand (to avoid infinite loops), throwing an error if that depth is exceeded.

**165. What is variadic tuple type?**
A tuple type that can spread other tuples or arrays into itself, allowing flexible-length tuple compositions.

**166. What are labeled tuple elements?**
Giving names to tuple positions for readability, e.g. `[start: number, end: number]`, without changing the actual type behavior.

**167. What is optional tuple element?**
A tuple element marked with `?`, meaning it can be omitted at the end of the tuple.

**168. What is rest element in tuple?**
A `...Type[]` element at the end of a tuple that allows a variable number of extra elements of that type.

**169. What is union type narrowing?**
Refining a union type down to one specific member using checks like `typeof`, `instanceof`, or custom type guards.

**170. What is intersection type?**
A type formed by combining multiple types with `&`, requiring the value to satisfy all of them simultaneously.

---

## Section 8: Utility Types

**171. What does `Partial<T>` do?**
Makes every property in a type optional.

**172. What does `Required<T>` do?**
Makes every property in a type required, removing any `?` optional markers.

**173. What does `Readonly<T>` do?**
Makes every property in a type readonly, so it can't be reassigned after creation.

**174. What does `Record<K, T>` do?**
Builds an object type where every key from `K` maps to a value of type `T`.

**175. What does `Pick<T, K>` do?**
Creates a new type containing only the selected properties `K` from type `T`.

**176. What does `Omit<T, K>` do?**
Creates a new type by removing the specified properties `K` from type `T`.

**177. What does `Exclude<T, U>` do?**
Removes types from a union `T` that are assignable to `U`.

**178. What does `Extract<T, U>` do?**
Keeps only the types from union `T` that are assignable to `U`.

**179. What does `NonNullable<T>` do?**
Removes `null` and `undefined` from a type, leaving only the meaningful values.

**180. What does `Parameters<T>` do?**
Extracts a function's parameter types as a tuple.

**181. What does `ReturnType<T>` do?**
Extracts the return type of a function.

**182. What does `ConstructorParameters<T>` do?**
Extracts a class constructor's parameter types as a tuple.

**183. What does `InstanceType<T>` do?**
Gets the instance type produced by a given class constructor.

**184. What does `ThisParameterType<T>` do?**
Extracts the type of the `this` parameter from a function type, if one is declared.

**185. What does `OmitThisParameter<T>` do?**
Removes the `this` parameter from a function type, leaving just the callable signature.

**186. What does `Awaited<T>` do?**
Unwraps the resolved value type of a `Promise`, even nested ones, recursively.

**187. What does `Uppercase<T>` do?**
Converts a string literal type to all uppercase.

**188. What does `Lowercase<T>` do?**
Converts a string literal type to all lowercase.

**189. What does `Capitalize<T>` do?**
Capitalizes the first letter of a string literal type.

**190. What does `Uncapitalize<T>` do?**
Lowercases the first letter of a string literal type.

---

## Section 9: Enums & Modules

**191. What is a numeric enum?**
An enum where each member automatically gets an incrementing number value, starting from 0 by default.

**192. How do you set custom enum values?**
Assign a specific value directly to a member, e.g. `Active = 1`; later members continue incrementing from there unless set too.

**193. What is a string enum?**
An enum where each member is explicitly assigned a string value instead of a number.

**194. What is a const enum?**
An enum that gets fully inlined at compile time, so no actual object exists in the compiled JavaScript output.

**195. What is reverse mapping in enums?**
The ability to get a numeric enum's member name back from its value, e.g. `Status[1]` returning `"Active"`.

**196. Can string enums have reverse mapping?**
No, reverse mapping only works for numeric enums; string enums don't generate that lookup.

**197. What is a heterogeneous enum?**
An enum mixing both string and numeric values in the same declaration — technically allowed but generally discouraged.

**198. How do you export types?**
Use the `export` keyword before an interface, type, or class so other files can import and use it.

**199. How do you import types?**
Use `import type { Name } from './file'` for type-only imports, which get removed from the compiled JS output.

**200. What is namespace?**
An older TypeScript feature for grouping related code under a single global name, mostly replaced by ES modules today.

**201. What is the difference between namespace and module?**
Namespaces group code within the global scope; modules are file-based and use standard `import`/`export` syntax.

**202. What is ambient declaration?**
Using `declare` to describe the shape of existing JavaScript code or libraries without providing an actual implementation.

**203. What is a `.d.ts` file?**
A type declaration file that only contains type information, with no runtime code, used to describe existing JS libraries.

**204. How do you create global type declarations?**
Use `declare global { ... }` inside a module file to add or extend types available everywhere in the project.

**205. What is triple-slash directive?**
A special comment like `/// <reference path="..." />` used to tell the compiler to include another file's type declarations.

---

## Section 10: Configuration & Tooling

**206. What is `tsconfig.json`?**
The configuration file that tells the TypeScript compiler how to compile your project — target version, strictness, output folder, etc.

**207. What does `target` option do?**
Sets which JavaScript version the compiled output should use, like `ES5` or `ES2020`.

**208. What does `module` option do?**
Determines the module system used in the compiled output, like `commonjs` or `ES6`.

**209. What does `strict` option do?**
Turns on all of TypeScript's strict type-checking options at once for maximum safety.

**210. What does `noImplicitAny` do?**
Forces an error whenever TypeScript can't infer a type and would otherwise silently default to `any`.

**211. What does `strictNullChecks` do?**
Makes `null` and `undefined` their own distinct types, preventing accidental assignment unless explicitly allowed.

**212. What does `outDir` option do?**
Specifies the folder where compiled JavaScript files should be placed.

**213. What does `rootDir` option do?**
Specifies the folder that contains your TypeScript source files.

**214. What does `include` option do?**
Lists which files or folders should be included when compiling the project.

**215. What does `exclude` option do?**
Lists which files or folders should be skipped during compilation, like `node_modules`.

**216. What does `esModuleInterop` do?**
Improves compatibility between CommonJS and ES module imports, allowing default-style imports to work smoothly.

**217. What does `skipLibCheck` do?**
Skips type-checking of all `.d.ts` declaration files to speed up compilation.

**218. What does `sourceMap` option do?**
Generates `.map` files that let you debug the original TypeScript code in the browser or editor.

**219. What does `declaration` option do?**
Generates `.d.ts` type declaration files alongside the compiled JavaScript, useful for library authors.

**220. What does `baseUrl` and `paths` do?**
Lets you set up custom shortcut import paths (aliases), like mapping `@components` to `src/components`.

---

## Section 11: Error Handling

**221. How do you handle union type errors?**
Use type guards like `typeof` or `instanceof` to narrow the union down before accessing type-specific properties.

**222. What is `strictFunctionTypes`?**
A compiler option that enforces stricter, more correct checking of function parameter compatibility.

**223. How do you fix "Object is possibly undefined"?**
Use optional chaining (`?.`) or add an explicit `if` check before accessing the property.

**224. What is non-null assertion operator?**
The `!` symbol placed after a value to tell TypeScript "I'm sure this isn't null or undefined," bypassing the check.

**225. How do you handle "Property does not exist on type"?**
Add the missing property to the type definition, or mark it optional if it's not always present.

**226. What is "Type 'X' is not assignable to type 'Y'"?**
A basic type mismatch error meaning the value's type doesn't match what's expected in that context.

**227. How do you fix "Cannot find module"?**
Install the module's type definitions (like `@types/package-name`) or write a custom `.d.ts` declaration file for it.

**228. What is "Argument of type X is not assignable to parameter of type Y"?**
It means the value you passed into a function doesn't match the type that function's parameter expects.

**229. How do you suppress TypeScript errors?**
Use `@ts-ignore` or `@ts-expect-error` comments above the line, though this should be avoided unless truly necessary.

**230. What is "Index signature is missing in type"?**
It means you're trying to access a property dynamically on a type that doesn't allow arbitrary keys — add an index signature to fix it.

---

## Section 12: Best Practices

**231. Should you use `any` type?**
Avoid it whenever possible since it disables type checking entirely; use `unknown` instead when the type is genuinely uncertain.

**232. When should you use `interface` vs `type`?**
Use `interface` for object shapes that might be extended later; use `type` for unions, intersections, and more complex compositions.

**233. Should you explicitly type everything?**
No, let TypeScript infer types when they're obvious — only add annotations when it improves clarity or is required.

**234. How do you handle external libraries without types?**
Install a matching `@types/` package if available, or write your own custom `.d.ts` declaration file.

**235. Should you use classes or interfaces for data structures?**
Use interfaces for pure data shapes; use classes only when you also need behavior (methods) attached to that data.

**236. When to use `readonly` modifier?**
Use it for properties that should never change after the object is first created, improving safety and predictability.

**237. Should you use enums or union types?**
Union types (like `"active" | "inactive"`) are usually simpler and lighter; enums suit more complex cases needing extra structure.

**238. How to structure large TypeScript projects?**
Organize code by feature/module, keep shared types in dedicated files, and use index files to simplify imports.

**239. Should you use `null` or `undefined`?**
Prefer `undefined` for values that simply weren't set yet; use `null` when you want to explicitly signal "intentionally empty."

**240. How to avoid circular dependencies?**
Move shared types/interfaces into their own separate file that both modules can import from independently.

**241. Should you use function declarations or arrow functions?**
Use regular function declarations for top-level named functions, and arrow functions for short callbacks or inline logic.

**242. How to handle API response types?**
Define clear interfaces describing the exact shape of the data your API returns, ideally matching the backend contract.

**243. Should you use `private` or `#` for class fields?**
`private` is a compile-time-only TypeScript feature; `#` is real JavaScript private field enforced at runtime — `#` is stricter.

**244. When to use generics vs `any`?**
Always prefer generics — they preserve type information and safety, while `any` throws all type checking away.

**245. Should you commit compiled JavaScript files?**
No, add the output folder (like `dist/`) to `.gitignore` and only commit your TypeScript source files.

---

## Section 13: Real-World Scenarios

**246. How to type API fetch response?**
Define an interface matching the expected JSON shape, then use it as the return type of your async fetch function.

**247. How to type form data?**
Create an interface mirroring the form's fields, then use it to type the object your submit handler receives.

**248. How to type Redux actions?**
Use a discriminated union of action objects, each with a distinct `type` string, so reducers can safely narrow them.

**249. How to type environment variables?**
Extend Node's `ProcessEnv` interface inside a global declaration file to describe the expected environment keys.

**250. How to type Express middleware?**
Use Express's built-in `Request`, `Response`, and `NextFunction` types for the middleware function's parameters.

**251. How to type Mongoose models?**
Create an interface extending Mongoose's `Document`, describing your schema fields, then pass it as a generic to the schema.

**252. How to type async/await with error handling?**
Wrap the `await` call in a `try/catch` block, and check `error instanceof Error` before accessing error properties safely.

**253. How to type localStorage wrapper?**
Wrap storage access in a generic class or function so `get`/`set` methods preserve the correct type for stored data.

**254. How to type event handlers in React?**
Use React's specific event types like `ChangeEvent<HTMLInputElement>` or `FormEvent<HTMLFormElement>` for handler parameters.

**255. How to type custom hooks?**
Either let TypeScript infer the return type automatically, or explicitly declare the returned object's shape for clarity.

**256. How to type HOC (Higher-Order Component)?**
Use a generic component type parameter so the wrapped component's original props are preserved and extended safely.

**257. How to type context API?**
Define an interface for the context's value shape, then create the context with that type (often allowing `undefined` as default).

**258. How to type dynamic imports?**
TypeScript infers the module's exported types automatically when you use `await import('./module')`.

**259. How to type WebSocket messages?**
Define a discriminated union of possible message shapes, each with a `type` field, so you can safely narrow and handle them.

**260. How to type pagination response?**
Create a generic interface like `PaginatedResponse<T>` holding `data: T[]` plus metadata fields like page and total count.
