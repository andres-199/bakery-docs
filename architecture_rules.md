# Architecture & Convictions

This document outlines the fundamental rules and architectural convictions governing the development of this project. Compliance is mandatory to ensure maintainability, scalability, and code quality.

## 1. Hexagonal Architecture (Ports & Adapters)

The system is organized into concentric layers where the business logic is the core and remains independent of external technologies.

- **Domain (Core):** Contains entities, value objects, and pure business rules. It has no external dependencies.
- **Application (Use Cases):** Orchestrates business logic. Defines **Ports** (interfaces) for communication with the outside world.
- **Infrastructure (Adapters):** Concrete implementations of the ports (DB, external APIs, web controllers, etc.).

## 2. SOLID Principles

Strict adherence to the five SOLID principles is required:

- **S**ingle Responsibility: Every function must have a single reason to change.
- **O**pen/Closed: Code should be open for extension but closed for modification.
- **L**iskov Substitution: Child objects should be able to replace those of the parent objects without altering functionality.
- **I**nterface Segregation: Specialized interfaces are better than a single general-purpose interface.
- **D**ependency Inversion: Depend on abstractions, not concrete implementations.

## 3. Clean Code & Quality

- **Readability:** Code must be self-explanatory. The use of descriptive names for variables, functions, and classes is imperative.
- **Small Functions:** Functions should perform a single task and be as short as possible.
- **DRY (Don't Repeat Yourself):** Avoid logic duplication.
- **KISS (Keep It Simple, Stupid):** Prioritize simplicity over unnecessary complexity.

## 4. Functional Programming

The use of functional paradigms is encouraged whenever possible:

- **Immutability:** Avoid state changes in objects after creation.
- **Pure Functions:** Prioritize functions that produce the same result for the same arguments without side effects.
- **Data Transformations:** Prefer the use of `map`, `filter`, `reduce`, and other declarative operators.

## 5. Dependency Injection

All dependencies must be injected. This facilitates decoupling and testability.

- NestJS's dependency injection engine is used for component management.
- Always inject interfaces (or abstract classes in TS) instead of concrete implementations into higher layers.

## 6. TypeScript and Strict Typing

- `strict` mode must always be enabled in `tsconfig.json`.
- Avoid using `any`. If a type is unknown, use `unknown` and validate it.
- Explicitly define interfaces and types for all entities and data flowing through the system.

## 7. Comments in Code

- **Golden Rule:** Never use comments in code.
- If the code is not clear enough to be understood without a comment, it must be refactored.
- Documentation explaining the "why" behind complex decisions should reside in design documents or ADRs, not in line comments.
## 8. Enums vs. Typed Constants

The use of native TypeScript `enum` is discouraged. Instead, use literal objects with `as const` and extract the type from them. This provides better compatibility with functional patterns and nominal typing.

```typescript
export const EntityTypes = {
  TYPE_A: 'TYPE_A',
  TYPE_B: 'TYPE_B',
} as const

export type EntityType = (typeof EntityTypes)[keyof typeof EntityTypes]
```
