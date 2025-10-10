# TypeScript Cheat Sheet

Quick reference for TypeScript syntax, types, and patterns. TypeScript adds static typing to JavaScript, helping catch errors early and improve code maintainability.

## Table of Contents

- [Basics](#basics)
- [Basic Types](#basic-types)
- [Type Annotations](#type-annotations)
- [Arrays and Tuples](#arrays-and-tuples)
- [Objects](#objects)
- [Functions](#functions)
- [Union and Intersection Types](#union-and-intersection-types)
- [Type Aliases and Interfaces](#type-aliases-and-interfaces)
- [Literal Types](#literal-types)
- [Enums](#enums)
- [Type Assertions](#type-assertions)
- [Generics](#generics)
- [Utility Types](#utility-types)
- [Classes](#classes)
- [Modules](#modules)
- [Narrowing](#narrowing)
- [Advanced Types](#advanced-types)
- [Declaration Files](#declaration-files)
- [tsconfig.json](#tsconfigjson)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)
- [Tools & References](#tools--references)

## Basics

```bash
# Install TypeScript
npm install -g typescript

# Check version
tsc --version

# Compile TypeScript file
tsc file.ts

# Watch mode
tsc --watch file.ts

# Initialize tsconfig.json
tsc --init
```

```typescript
// TypeScript is a superset of JavaScript
// All valid JavaScript is valid TypeScript

// Type inference - TypeScript infers types
let message = "Hello"; // inferred as string
message = 42; // Error: Type 'number' not assignable to 'string'
```

## Basic Types

```typescript
// Primitives
let isDone: boolean = true;
let age: number = 30;
let name: string = "Alice";
let notDefined: undefined = undefined;
let notPresent: null = null;

// Any (avoid when possible)
let anything: any = 42;
anything = "now a string";
anything = true;

// Unknown (safer than any)
let value: unknown = 42;
value = "string";
// Must narrow type before using
if (typeof value === "string") {
  console.log(value.toUpperCase());
}

// Void (function returns nothing)
function logMessage(message: string): void {
  console.log(message);
}

// Never (function never returns)
function throwError(message: string): never {
  throw new Error(message);
}

function infiniteLoop(): never {
  while (true) {}
}

// BigInt and Symbol
let big: bigint = 100n;
let sym: symbol = Symbol("key");
```

## Type Annotations

```typescript
// Variables
let firstName: string = "Alice";
let age: number = 30;

// Type inference (no annotation needed)
let lastName = "Smith"; // inferred as string

// Multiple types (union)
let id: string | number = 123;
id = "ABC123";

// Function parameters and return types
function greet(name: string): string {
  return `Hello, ${name}!`;
}

// Optional parameters
function buildName(firstName: string, lastName?: string): string {
  return lastName ? `${firstName} ${lastName}` : firstName;
}

// Default parameters
function multiply(a: number, b: number = 1): number {
  return a * b;
}

// Rest parameters
function sum(...numbers: number[]): number {
  return numbers.reduce((acc, n) => acc + n, 0);
}
```

## Arrays and Tuples

```typescript
// Arrays
let numbers: number[] = [1, 2, 3];
let strings: Array<string> = ["a", "b", "c"];

// Array of objects
let users: { name: string; age: number }[] = [
  { name: "Alice", age: 30 },
  { name: "Bob", age: 25 },
];

// Tuples (fixed-length arrays with known types)
let tuple: [string, number] = ["Alice", 30];
let rgb: [number, number, number] = [255, 0, 0];

// Tuple with optional elements
let point: [number, number, number?] = [10, 20];

// Rest in tuples
let scores: [string, ...number[]] = ["Alice", 90, 85, 92];

// Readonly arrays
let readonlyNumbers: readonly number[] = [1, 2, 3];
// readonlyNumbers.push(4);  // Error
```

## Objects

```typescript
// Object type annotation
let person: { name: string; age: number } = {
  name: "Alice",
  age: 30,
};

// Optional properties
let user: { name: string; age?: number } = {
  name: "Bob",
};

// Readonly properties
let point: { readonly x: number; readonly y: number } = {
  x: 10,
  y: 20,
};
// point.x = 30;  // Error

// Index signatures (dynamic keys)
let scores: { [key: string]: number } = {
  math: 90,
  science: 85,
};

// Mixed index signatures
interface StringArray {
  [index: number]: string;
}

let myArray: StringArray = ["Alice", "Bob"];
```

## Functions

```typescript
// Function type annotation
let add: (a: number, b: number) => number;
add = (x, y) => x + y;

// Function expressions
const multiply = function (a: number, b: number): number {
  return a * b;
};

// Arrow functions
const divide = (a: number, b: number): number => a / b;

// Void return type
const logMessage = (message: string): void => {
  console.log(message);
};

// Function overloads
function getValue(id: number): string;
function getValue(id: string): number;
function getValue(id: number | string): string | number {
  if (typeof id === "number") {
    return "Value for " + id;
  } else {
    return id.length;
  }
}

// this parameter
interface User {
  name: string;
  greet(this: User): void;
}

const user: User = {
  name: "Alice",
  greet() {
    console.log(`Hello, ${this.name}`);
  },
};
```

## Union and Intersection Types

```typescript
// Union types (OR)
let id: string | number;
id = 123;
id = "ABC";

function printId(id: string | number): void {
  console.log(`ID: ${id}`);
}

// Union with literals
type Status = "pending" | "approved" | "rejected";
let status: Status = "pending";

// Intersection types (AND)
interface Person {
  name: string;
}

interface Employee {
  employeeId: number;
}

type Staff = Person & Employee;

const staff: Staff = {
  name: "Alice",
  employeeId: 123,
};

// Combining multiple types
type Admin = Person & Employee & { privileges: string[] };
```

## Type Aliases and Interfaces

```typescript
// Type alias
type Point = {
  x: number;
  y: number;
};

type ID = string | number;

// Interface
interface User {
  name: string;
  age: number;
  email?: string;
}

// Extending interfaces
interface Employee extends User {
  employeeId: number;
  department: string;
}

// Multiple inheritance
interface Manager extends Employee, Person {
  team: string[];
}

// Type alias vs Interface
// - Type aliases can represent primitives, unions, tuples
// - Interfaces can be extended and merged
// - Prefer interfaces for objects that may be extended

// Interface merging (declaration merging)
interface Window {
  title: string;
}

interface Window {
  content: string;
}

// Window now has both title and content

// Callable interfaces
interface SearchFunc {
  (source: string, subString: string): boolean;
}

const mySearch: SearchFunc = (src, sub) => {
  return src.includes(sub);
};
```

## Literal Types

```typescript
// String literals
let direction: "north" | "south" | "east" | "west";
direction = "north";
// direction = "up";  // Error

// Numeric literals
let roll: 1 | 2 | 3 | 4 | 5 | 6;
roll = 3;

// Boolean literals
let success: true = true;
// success = false;  // Error

// Combining with union types
function compare(a: string, b: string): -1 | 0 | 1 {
  return a === b ? 0 : a > b ? 1 : -1;
}

// Literal types in objects
type RequestOptions = {
  method: "GET" | "POST" | "PUT" | "DELETE";
  headers?: Record<string, string>;
};

// const assertions
let x = "hello" as const; // type: "hello"
let arr = [10, 20] as const; // type: readonly [10, 20]

const config = {
  endpoint: "https://api.example.com",
  timeout: 5000,
} as const;
// config properties are readonly
```

## Enums

```typescript
// Numeric enums
enum Direction {
  Up, // 0
  Down, // 1
  Left, // 2
  Right, // 3
}

let dir: Direction = Direction.Up;

// With initializers
enum Status {
  Active = 1,
  Inactive = 2,
  Pending = 3,
}

// String enums
enum Color {
  Red = "RED",
  Green = "GREEN",
  Blue = "BLUE",
}

// Heterogeneous enums (avoid)
enum Mixed {
  No = 0,
  Yes = "YES",
}

// Const enums (inline at compile time)
const enum Sizes {
  Small = 1,
  Medium = 2,
  Large = 3,
}

let size = Sizes.Small; // Compiled to: let size = 1;

// Reverse mapping (numeric enums only)
enum Role {
  Admin = 1,
  User = 2,
}

let roleName = Role[1]; // "Admin"
```

## Type Assertions

```typescript
// Type assertion (angle bracket syntax)
let someValue: unknown = "this is a string";
let strLength: number = (<string>someValue).length;

// Type assertion (as syntax - preferred in JSX)
let value: unknown = "hello";
let length: number = (value as string).length;

// Asserting to more specific type
interface Cat {
  meow(): void;
}

interface Dog {
  bark(): void;
}

function getAnimal(): Cat | Dog {
  return { meow: () => console.log("Meow") };
}

const animal = getAnimal();
(animal as Cat).meow();

// Non-null assertion operator
function getValue(id: string | null): string {
  // Tell TypeScript this is definitely not null
  return id!.toUpperCase();
}

// Double assertion (escape hatch - use sparingly)
const num = "123" as unknown as number; // Not recommended!

// Const assertions
let x = "hello" as const;
let arr = [1, 2, 3] as const;
```

## Generics

```typescript
// Generic function
function identity<T>(arg: T): T {
  return arg;
}

let output1 = identity<string>("hello");
let output2 = identity(42); // type inferred

// Generic with constraints
interface HasLength {
  length: number;
}

function logLength<T extends HasLength>(arg: T): void {
  console.log(arg.length);
}

logLength("hello");
logLength([1, 2, 3]);
// logLength(42);  // Error: number doesn't have length

// Generic interfaces
interface GenericIdentityFn<T> {
  (arg: T): T;
}

let myIdentity: GenericIdentityFn<number> = identity;

// Generic classes
class GenericNumber<T> {
  zeroValue: T;
  add: (x: T, y: T) => T;
}

let myNumber = new GenericNumber<number>();
myNumber.zeroValue = 0;
myNumber.add = (x, y) => x + y;

// Multiple type parameters
function pair<T, U>(first: T, second: U): [T, U] {
  return [first, second];
}

let result = pair("hello", 42); // [string, number]

// Generic constraints with keyof
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

let person = { name: "Alice", age: 30 };
let name = getProperty(person, "name"); // string
let age = getProperty(person, "age"); // number

// Default generic parameters
interface Container<T = string> {
  value: T;
}

let stringContainer: Container = { value: "hello" };
let numberContainer: Container<number> = { value: 42 };
```

## Utility Types

```typescript
// Partial<T> - makes all properties optional
interface User {
  name: string;
  age: number;
  email: string;
}

type PartialUser = Partial<User>;
// { name?: string; age?: number; email?: string; }

function updateUser(user: User, updates: Partial<User>): User {
  return { ...user, ...updates };
}

// Required<T> - makes all properties required
type RequiredUser = Required<PartialUser>;

// Readonly<T> - makes all properties readonly
type ReadonlyUser = Readonly<User>;

// Record<K, T> - construct object type with keys K and values T
type Roles = "admin" | "user" | "guest";
type RolePermissions = Record<Roles, string[]>;

const permissions: RolePermissions = {
  admin: ["read", "write", "delete"],
  user: ["read", "write"],
  guest: ["read"],
};

// Pick<T, K> - pick specific properties
type UserPreview = Pick<User, "name" | "email">;
// { name: string; email: string; }

// Omit<T, K> - omit specific properties
type UserWithoutEmail = Omit<User, "email">;
// { name: string; age: number; }

// Exclude<T, U> - exclude types from union
type T1 = Exclude<"a" | "b" | "c", "a" | "b">; // "c"

// Extract<T, U> - extract types from union
type T2 = Extract<"a" | "b" | "c", "a" | "f">; // "a"

// NonNullable<T> - remove null and undefined
type T3 = NonNullable<string | number | null | undefined>; // string | number

// ReturnType<T> - get function return type
function getUser() {
  return { name: "Alice", age: 30 };
}

type UserReturn = ReturnType<typeof getUser>;
// { name: string; age: number; }

// Parameters<T> - get function parameter types as tuple
function createUser(name: string, age: number) {}
type CreateUserParams = Parameters<typeof createUser>;
// [name: string, age: number]

// Awaited<T> - unwrap Promise type
type A = Awaited<Promise<string>>; // string
type B = Awaited<Promise<Promise<number>>>; // number
```

## Classes

```typescript
// Basic class
class Person {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  greet(): string {
    return `Hello, I'm ${this.name}`;
  }
}

// Access modifiers
class Employee {
  public name: string; // accessible everywhere
  private salary: number; // only within class
  protected department: string; // within class and subclasses

  constructor(name: string, salary: number, department: string) {
    this.name = name;
    this.salary = salary;
    this.department = department;
  }

  getSalary(): number {
    return this.salary;
  }
}

// Shorthand constructor
class User {
  constructor(public name: string, public age: number, private email: string) {}
}

// Readonly properties
class Point {
  readonly x: number;
  readonly y: number;

  constructor(x: number, y: number) {
    this.x = x;
    this.y = y;
  }
}

// Inheritance
class Manager extends Employee {
  constructor(
    name: string,
    salary: number,
    department: string,
    public team: string[]
  ) {
    super(name, salary, department);
  }

  getTeamSize(): number {
    return this.team.length;
  }
}

// Abstract classes
abstract class Shape {
  abstract getArea(): number;

  describe(): string {
    return `Area: ${this.getArea()}`;
  }
}

class Circle extends Shape {
  constructor(public radius: number) {
    super();
  }

  getArea(): number {
    return Math.PI * this.radius ** 2;
  }
}

// Static members
class MathUtils {
  static PI = 3.14159;

  static calculateCircumference(diameter: number): number {
    return diameter * MathUtils.PI;
  }
}

// Implementing interfaces
interface Printable {
  print(): void;
}

class Document implements Printable {
  constructor(public content: string) {}

  print(): void {
    console.log(this.content);
  }
}

// Getters and setters
class Temperature {
  private _celsius: number = 0;

  get celsius(): number {
    return this._celsius;
  }

  set celsius(value: number) {
    this._celsius = value;
  }

  get fahrenheit(): number {
    return (this._celsius * 9) / 5 + 32;
  }

  set fahrenheit(value: number) {
    this._celsius = ((value - 32) * 5) / 9;
  }
}
```

## Modules

```typescript
// Exporting
// math.ts
export function add(a: number, b: number): number {
  return a + b;
}

export const PI = 3.14159;

export interface Point {
  x: number;
  y: number;
}

// Default export
export default class Calculator {
  add(a: number, b: number): number {
    return a + b;
  }
}

// Importing
// app.ts
import Calculator, { add, PI, Point } from "./math";
import * as Math from "./math";

const calc = new Calculator();
const result = add(1, 2);

// Re-exporting
export { add, PI } from "./math";
export * from "./utils";

// Type-only imports/exports
import type { User } from "./types";
export type { User };
```

## Narrowing

```typescript
// typeof narrowing
function printValue(value: string | number) {
  if (typeof value === "string") {
    console.log(value.toUpperCase());
  } else {
    console.log(value.toFixed(2));
  }
}

// Truthiness narrowing
function printLength(str: string | null) {
  if (str) {
    console.log(str.length);
  } else {
    console.log("No string provided");
  }
}

// Equality narrowing
function compare(x: string | number, y: string | boolean) {
  if (x === y) {
    // x and y are both string
    console.log(x.toUpperCase(), y.toUpperCase());
  }
}

// in operator narrowing
interface Fish {
  swim(): void;
}

interface Bird {
  fly(): void;
}

function move(animal: Fish | Bird) {
  if ("swim" in animal) {
    animal.swim();
  } else {
    animal.fly();
  }
}

// instanceof narrowing
function logValue(value: Date | string) {
  if (value instanceof Date) {
    console.log(value.toISOString());
  } else {
    console.log(value.toUpperCase());
  }
}

// Type predicates
function isFish(animal: Fish | Bird): animal is Fish {
  return (animal as Fish).swim !== undefined;
}

function move2(animal: Fish | Bird) {
  if (isFish(animal)) {
    animal.swim();
  } else {
    animal.fly();
  }
}

// Discriminated unions
interface Circle {
  kind: "circle";
  radius: number;
}

interface Rectangle {
  kind: "rectangle";
  width: number;
  height: number;
}

type Shape = Circle | Rectangle;

function getArea(shape: Shape): number {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;
    case "rectangle":
      return shape.width * shape.height;
  }
}

// Exhaustiveness checking
function assertNever(value: never): never {
  throw new Error(`Unexpected value: ${value}`);
}

function getArea2(shape: Shape): number {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;
    case "rectangle":
      return shape.width * shape.height;
    default:
      return assertNever(shape); // Error if we missed a case
  }
}
```

## Advanced Types

```typescript
// Mapped types
type Readonly<T> = {
  readonly [P in keyof T]: T[P];
};

type Nullable<T> = {
  [P in keyof T]: T[P] | null;
};

// Conditional types
type IsString<T> = T extends string ? true : false;
type A = IsString<string>; // true
type B = IsString<number>; // false

// Conditional type with infer
type ReturnType<T> = T extends (...args: any[]) => infer R ? R : never;

type Unpromisify<T> = T extends Promise<infer U> ? U : T;
type Result = Unpromisify<Promise<string>>; // string

// Template literal types
type EmailEvent = `${string}@${string}.${string}`;
let email: EmailEvent = "user@example.com";

type EventName = "click" | "focus" | "blur";
type EventHandler = `on${Capitalize<EventName>}`;
// "onClick" | "onFocus" | "onBlur"

// Index accessed types
type Person = {
  name: string;
  age: number;
  location: string;
};

type Age = Person["age"]; // number
type NameOrAge = Person["name" | "age"]; // string | number
type AllValues = Person[keyof Person]; // string | number

// Recursive types
type Json = string | number | boolean | null | Json[] | { [key: string]: Json };

// Brand types (nominal typing)
type Brand<K, T> = K & { __brand: T };
type USD = Brand<number, "USD">;
type EUR = Brand<number, "EUR">;

function addDollars(a: USD, b: USD): USD {
  return (a + b) as USD;
}
```

## Declaration Files

```typescript
// yourlib.d.ts
declare module "your-untyped-lib" {
  export function doSomething(value: string): number;
  export const version: string;
}

// Global declarations
declare global {
  interface Window {
    myCustomProperty: string;
  }

  var MY_GLOBAL: string;
}

// Ambient declarations
declare const jQuery: (selector: string) => any;

// Module augmentation
import { Observable } from "rxjs";

declare module "rxjs" {
  interface Observable<T> {
    customOperator(): Observable<T>;
  }
}
```

## tsconfig.json

```json
{
  "compilerOptions": {
    // Type Checking
    "strict": true, // Enable all strict type checking options
    "noImplicitAny": true, // Error on expressions with implied 'any'
    "strictNullChecks": true, // Strict null checking
    "strictFunctionTypes": true, // Strict function type checking
    "noUnusedLocals": true, // Error on unused local variables
    "noUnusedParameters": true, // Error on unused parameters

    // Modules
    "module": "ESNext", // Module system
    "moduleResolution": "node", // Module resolution strategy
    "esModuleInterop": true, // Emit __importStar and __importDefault helpers
    "allowSyntheticDefaultImports": true,

    // Emit
    "target": "ES2020", // JavaScript version
    "outDir": "./dist", // Output directory
    "rootDir": "./src", // Root directory of source files
    "sourceMap": true, // Generate source maps
    "declaration": true, // Generate .d.ts files
    "removeComments": true, // Remove comments from output

    // Interop Constraints
    "isolatedModules": true, // Ensure each file can be transpiled independently
    "allowJs": true, // Allow JavaScript files
    "checkJs": false, // Type-check JavaScript files

    // Advanced
    "skipLibCheck": true, // Skip type checking of declaration files
    "forceConsistentCasingInFileNames": true,
    "resolveJsonModule": true, // Allow importing JSON files
    "jsx": "react" // JSX support (for React)
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist"]
}
```

## Best Practices

- Use `strict` mode in tsconfig.json for maximum type safety
- Prefer `interface` for object shapes, `type` for unions/intersections
- Use `unknown` instead of `any` when type is truly unknown
- Avoid type assertions unless absolutely necessary
- Use `const` assertions for literal types
- Leverage utility types instead of creating custom mapped types
- Use discriminated unions for complex state
- Enable `noImplicitAny` and fix errors instead of using `any`
- Use type predicates for complex type narrowing
- Document complex types with JSDoc comments

```typescript
// Good practices

// Use unknown instead of any
function processValue(value: unknown) {
  if (typeof value === "string") {
    return value.toUpperCase();
  }
  return value;
}

// Discriminated unions for state
type State =
  | { status: "loading" }
  | { status: "success"; data: string }
  | { status: "error"; error: Error };

function handleState(state: State) {
  switch (state.status) {
    case "loading":
      return "Loading...";
    case "success":
      return state.data;
    case "error":
      return state.error.message;
  }
}

// Const assertions for configuration
const CONFIG = {
  api: "https://api.example.com",
  timeout: 5000,
  retries: 3,
} as const;

// Use readonly for immutable data
function processArray(arr: readonly number[]): number {
  // arr.push(1);  // Error: cannot modify readonly array
  return arr.reduce((sum, n) => sum + n, 0);
}
```

## Troubleshooting

- **Type 'X' is not assignable to type 'Y'**: Check if types match; use union types or type assertions if needed
- **Property 'X' does not exist on type 'Y'**: Type might be too broad; use type narrowing or optional chaining
- **Cannot find module**: Check import paths, tsconfig paths, and module resolution settings
- **Object is possibly 'undefined'**: Use optional chaining (`?.`) or null check before accessing
- **Type 'any' implicitly has an 'any' type**: Add explicit type annotations or enable `noImplicitAny`
- **Cannot redeclare block-scoped variable**: Variable declared multiple times; check imports and scopes
- **'this' implicitly has type 'any'**: Add explicit `this` parameter or use arrow functions

```typescript
// Common fixes

// Optional chaining
const value = obj?.property?.nestedProperty;

// Nullish coalescing
const result = value ?? defaultValue;

// Type guards
function isString(value: unknown): value is string {
  return typeof value === "string";
}

// Non-null assertion (use sparingly)
const element = document.getElementById("app")!;

// Type assertion (when you know better than TypeScript)
const input = document.getElementById("input") as HTMLInputElement;
```

## Tools & References

- **Official TypeScript Docs**: https://www.typescriptlang.org/docs/
- **TypeScript Playground**: Test and share TypeScript code
- **DefinitelyTyped**: Type definitions for JavaScript libraries (@types)
- **ts-node**: Run TypeScript directly without compilation
- **ESLint with TypeScript**: Linting for TypeScript
- **Prettier**: Code formatting
- **Type Challenges**: Practice TypeScript type system

---

Quick tip: Use the TypeScript Playground to experiment with types and see the compiled JavaScript output. Enable "strict" mode to catch more errors early.
