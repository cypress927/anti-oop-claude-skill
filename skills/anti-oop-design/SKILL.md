---
name: anti-oop-design
description: >-
  Architecture by aggregation: decouple pure functions from side effects. Group
  related logic, split into pure functions and I/O, name last from what emerges,
  keep growing data out of computation.
---

## Core Idea

A program has only two kinds of functions: pure functions (computation) and side-effect functions (storage). Architecture is not designed upfront — it is discovered by grouping related business variables and logic together, then separating them into pure computation and side effects.

### Principles

1. **Two kinds only** — pure (compute) and side-effect (store). "Orchestration" is a composition pattern, not a third category.

2. **Aggregate first, separate second** — gather all related business variables and logic before deciding what is pure and what is a side effect.

3. **Name last** — do not start by defining `User`, `Book`, or any shared type. Write concrete logic first. Extract shared types only when the same structure actually repeats.

4. **Exact dependencies** — each pure function receives only the fields it uses. If it only needs `score`, pass `score: number`, not the entire user object.

5. **Data growth isolation** — identify data that will grow (users, books, loans). No business logic depends on data size. Arrays, lists, pagination never appear in pure functions. The storage layer aggregates, counts, and filters before passing finite values to computation.

### Step-by-Step Process

1. Gather scattered business variables and conditions into one place — this is discovery, not design
2. Split the cluster into two piles: pure functions (no I/O, no mutation, no `new Date()`) vs side-effect functions (I/O, persistence, external state)
3. Observe what each pile contains, then name it — the name comes from what emerged, not from what you planned
4. One step at a time. Verify after each change. Step back if wrong.

### Example Structure

```
src/
  domain/
    decisions/          # pure functions — business rules
      borrowDecision.ts
      returnDecision.ts
      renewDecision.ts
      types.ts          # shared result types (only after repetition)
    utils.ts            # shared pure utilities
  repository/           # side-effect functions — I/O, storage
    interfaces.ts
    Database.ts
  service/              # orchestration
    BorrowService.ts
  index.ts
```

### Usage

Apply this skill when starting a new feature or refactoring:

1. Identify the business rule to implement
2. Write it as a pure function first — plain data in, decision out
3. Define I/O around what the pure function needs
4. Let the service layer be thin orchestration between I/O and pure functions
5. Only extract shared types after seeing actual repetition

Do NOT start by defining class hierarchies, shared types, or layered architectures. Let the structure emerge from the pure functions.
