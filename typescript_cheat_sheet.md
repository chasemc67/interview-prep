# TypeScript Crash Course (LeetCode-Style)

A concise refresher on essential TypeScript types, syntax, and patterns commonly used in coding interviews.

## Quick Reference

### Most Common Types

```typescript
// Primitives
string, number, boolean, null, undefined, any, void, never

// Collections
Array<T>, [T, U], Set<T>, Map<K, V>

// Objects
interface, type, class
```

### Common Patterns

```typescript
// Two Pointers
let left = 0,
  right = arr.length - 1;

// Sliding Window
let window = arr.slice(0, k);

// Binary Search
let mid = Math.floor((left + right) / 2);
```

### Quick Lookup

| Operation          | Syntax                  |
| ------------------ | ----------------------- |
| Type Assertion     | `value as Type`         |
| Optional Chaining  | `obj?.prop`             |
| Nullish Coalescing | `value ?? defaultValue` |
| Spread Operator    | `{...obj1, ...obj2}`    |
| Destructuring      | `const {prop} = obj`    |

---

## 1. Basic Types

```typescript
// Primitive types
let isDone: boolean = false;
let count: number = 42;
let name: string = "TypeScript";
let nothing: null = null;
let notDefined: undefined = undefined;

// Arrays
let numbers: number[] = [1, 2, 3];
let strings: Array<string> = ["a", "b", "c"];

// Tuples
let tuple: [string, number] = ["hello", 10];

// Any (avoid when possible)
let anything: any = "can be anything";

// Void (for functions that don't return)
function logMessage(): void {
  console.log("Hello");
}

// Never (for functions that never return)
function throwError(): never {
  throw new Error("Error!");
}
```

## 2. Type Aliases and Interfaces

```typescript
// Type alias
type Point = {
  x: number;
  y: number;
};

// Interface
interface User {
  id: number;
  name: string;
  email?: string; // Optional property
  readonly createdAt: Date; // Readonly property
}

// Extending interfaces
interface Admin extends User {
  permissions: string[];
}

// Implementing interface
class AdminUser implements Admin {
  id: number;
  name: string;
  permissions: string[];
  createdAt: Date;
}
```

## 3. Arrays and Array Methods

```typescript
const arr: number[] = [1, 2, 3, 4, 5];

// Common array methods
arr.push(6); // Add to end
arr.pop(); // Remove from end
arr.unshift(0); // Add to beginning
arr.shift(); // Remove from beginning
arr.slice(1, 3); // Get subarray
arr.splice(1, 2); // Remove elements
arr.indexOf(3); // Find index
arr.includes(3); // Check existence
arr.sort(); // Sort array
arr.reverse(); // Reverse array

// Functional methods
arr.map((x) => x * 2); // Transform each element
arr.filter((x) => x > 2); // Filter elements
arr.reduce((acc, x) => acc + x, 0); // Reduce to single value
arr.forEach((x) => console.log(x)); // Execute for each element
arr.some((x) => x > 3); // Check if any element matches
arr.every((x) => x > 0); // Check if all elements match
```

## 4. Destructuring

```typescript
// Array destructuring
const [first, second, ...rest] = [1, 2, 3, 4, 5];
// first = 1, second = 2, rest = [3, 4, 5]

// Object destructuring
const user = { id: 1, name: "John", age: 30 };
const { id, name, age } = user;
// id = 1, name = "John", age = 30

// Renaming during destructuring
const { name: userName } = user;
// userName = "John"

// Default values
const { name = "Anonymous" } = user;
```

## 5. Generics

```typescript
// Generic function
function identity<T>(arg: T): T {
  return arg;
}

// Generic interface
interface Box<T> {
  value: T;
}

// Generic class
class Stack<T> {
  private items: T[] = [];

  push(item: T): void {
    this.items.push(item);
  }

  pop(): T | undefined {
    return this.items.pop();
  }
}
```

## 6. Built-in Utility Types

```typescript
// Partial<T> - Make all properties optional
type PartialUser = Partial<User>;

// Required<T> - Make all properties required
type RequiredUser = Required<User>;

// Readonly<T> - Make all properties readonly
type ReadonlyUser = Readonly<User>;

// Pick<T, K> - Pick specific properties
type UserName = Pick<User, "name">;

// Omit<T, K> - Omit specific properties
type UserWithoutId = Omit<User, "id">;

// Record<K, T> - Create object type with specific keys and value type
type UserMap = Record<string, User>;
```

## 7. Common Data Structures

```typescript
// Set
const set = new Set<number>();
set.add(1);
set.has(1);
set.delete(1);
set.size;

// Map
const map = new Map<string, number>();
map.set("one", 1);
map.get("one");
map.has("one");
map.delete("one");
map.size;

// Queue (using array)
const queue: number[] = [];
queue.push(1); // enqueue
queue.shift(); // dequeue

// Stack (using array)
const stack: number[] = [];
stack.push(1); // push
stack.pop(); // pop
```

## 8. String Operations

```typescript
const str = "Hello, TypeScript";

// Common string methods
str.length;
str.charAt(0);
str.substring(1, 4);
str.slice(1, 4);
str.split(",");
str.replace("TypeScript", "World");
str.toLowerCase();
str.toUpperCase();
str.trim();
str.includes("Type");
str.indexOf("Type");
str.startsWith("Hello");
str.endsWith("Script");
```

## 9. Math and Number Operations

```typescript
// Math operations
Math.abs(-5);
Math.ceil(4.2);
Math.floor(4.8);
Math.round(4.5);
Math.max(1, 2, 3);
Math.min(1, 2, 3);
Math.random();
Math.sqrt(16);
Math.pow(2, 3);

// Number methods
Number.isInteger(5);
Number.isNaN(NaN);
Number.parseInt("42");
Number.parseFloat("42.5");
```

## 10. Additional Tips

```typescript
// Type assertions
const value: any = "hello";
const strLength: number = (value as string).length;

// Optional chaining
const user = { address: { street: "Main" } };
const street = user?.address?.street;

// Nullish coalescing
const name = user?.name ?? "Anonymous";

// Template literals
const greeting = `Hello, ${name}!`;

// Spread operator
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5];

const obj1 = { a: 1, b: 2 };
const obj2 = { ...obj1, c: 3 };
```

## 11. Common Interview Patterns

```typescript
// Two pointers
function twoSum(nums: number[], target: number): number[] {
  let left = 0;
  let right = nums.length - 1;
  while (left < right) {
    const sum = nums[left] + nums[right];
    if (sum === target) return [left, right];
    if (sum < target) left++;
    else right--;
  }
  return [];
}

// Sliding window
function maxSubarray(nums: number[], k: number): number {
  let maxSum = 0;
  let windowSum = 0;
  for (let i = 0; i < k; i++) {
    windowSum += nums[i];
  }
  maxSum = windowSum;
  for (let i = k; i < nums.length; i++) {
    windowSum = windowSum - nums[i - k] + nums[i];
    maxSum = Math.max(maxSum, windowSum);
  }
  return maxSum;
}

// Binary search
function binarySearch(nums: number[], target: number): number {
  let left = 0;
  let right = nums.length - 1;
  while (left <= right) {
    const mid = Math.floor((left + right) / 2);
    if (nums[mid] === target) return mid;
    if (nums[mid] < target) left = mid + 1;
    else right = mid - 1;
  }
  return -1;
}
```

## 12. Best Practices

### Common Pitfalls to Avoid

```typescript
// ❌ Avoid using 'any' type
let data: any = getData(); // Bad
let data: unknown = getData(); // Better

// ❌ Don't use type assertions without validation
const value = someValue as string; // Bad
if (typeof someValue === "string") {
  // Better
  const value = someValue;
}

// ❌ Avoid non-null assertions
const element = document.getElementById("id")!; // Bad
const element = document.getElementById("id");
if (element) {
  // Better
  // Use element
}
```

### Performance Considerations

```typescript
// Use const for immutable values
const PI = 3.14; // Better than let

// Prefer type aliases for complex types
type User = {
  id: number;
  name: string;
};

// Use readonly for immutable arrays/objects
const readonlyArray: readonly number[] = [1, 2, 3];

// Use proper type narrowing
function processValue(value: string | number) {
  if (typeof value === "string") {
    // Type is narrowed to string
  }
}
```

### Code Style Guidelines

```typescript
// Use consistent naming conventions
interface IUser {
  // Prefix interfaces with I
  id: number;
  name: string;
}

// Use PascalCase for types and interfaces
type UserProfile = {
  // ...
};

// Use camelCase for variables and functions
const getUserData = () => {
  // ...
};

// Use meaningful type names
type UserId = number; // Better than just 'number'

// Document complex types
/**
 * Represents a user in the system
 * @property id - Unique identifier
 * @property name - User's full name
 */
interface User {
  id: number;
  name: string;
}
```
