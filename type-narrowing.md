# What Is Type Narrowing in TypeScript?

## Introduction

TypeScript allows a variable to hold more than one type through union types. A union is useful, but it also means that an operation may not be safe for every possible member of that union. Type narrowing is the process of checking a value and reducing its possible types before using it. It helps us write safer code without relying on `any` or unsafe assumptions.

## Detailed Explanation

The `typeof` operator is useful for primitive values. For example, a function that accepts a string or number can check the value before choosing an operation:

```ts
function formatValue(value: string | number): string {
  if (typeof value === "string") {
    return value.trim().toLowerCase();
  }

  return (value * 10).toString();
}
```

Inside the first branch, TypeScript knows that `value` is a string. In the other branch, it knows that the value is a number.

Use `instanceof` to distinguish instances of classes such as `Date`:

```ts
function showDate(value: Date | string): string {
  if (value instanceof Date) {
    return value.toISOString();
  }

  return new Date(value).toISOString();
}
```

The `in` operator checks whether an object contains a property. It is especially helpful with object unions:

```ts
type Bird = { fly: () => void };
type Fish = { swim: () => void };

function move(animal: Bird | Fish): void {
  if ("fly" in animal) {
    animal.fly();
  } else {
    animal.swim();
  }
}
```

After the check, TypeScript identifies the matching object shape and permits the correct method call.

## Conclusion

Type narrowing makes union types practical and safe. Use `typeof` for primitive types, `instanceof` for class instances, and `in` for checking object properties. These checks help the compiler understand your intent and catch invalid operations early.
