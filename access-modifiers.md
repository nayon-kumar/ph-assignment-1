# Access Modifiers in TypeScript Object-Oriented Programming

## Introduction

Classes group data and behavior into reusable structures. In TypeScript, access modifiers control where class properties and methods can be accessed. The main modifiers are `public`, `private`, and `protected`; `readonly` controls whether a property can be reassigned after initialization. Choosing the right modifier helps protect an object's internal state.

## Detailed Explanation

A `public` member is accessible from anywhere, including outside the class. It is the default when no modifier is written. A `private` member can only be accessed inside the class where it is declared:

```ts
class Employee {
  public name: string;
  private salary: number;

  constructor(name: string, salary: number) {
    this.name = name;
    this.salary = salary;
  }

  getSalary(): number {
    return this.salary;
  }
}
```

Code outside `Employee` can read `name`, but it cannot directly read `salary`. The public method provides controlled access to the private value.

A `protected` member is available inside its declaring class and its subclasses, but not through an external object:

```ts
class Manager extends Employee {
  describe(): string {
    return `Manager: ${this.name}`;
  }
}
```

Here, the subclass can access the inherited `name` property if it is declared `protected`.

The `readonly` modifier prevents reassignment after the property is initialized, usually in its declaration or constructor:

```ts
class Account {
  constructor(public readonly accountId: string) {}
}
```

The account ID can be read later, but code cannot assign a different value to it.

## Conclusion

Use `public` for intentionally exposed members, `private` to keep implementation details inside a class, and `protected` when subclasses need access. Use `readonly` for values that should not be reassigned. Together, these modifiers support encapsulation and clearer OOP design.
