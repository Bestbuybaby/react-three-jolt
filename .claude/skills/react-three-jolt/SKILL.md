```markdown
# react-three-jolt Development Patterns

> Auto-generated skill from repository analysis

## Overview
This skill teaches you the core development patterns, coding conventions, and automation workflows used in the `react-three-jolt` TypeScript codebase. You'll learn how to structure files, write and organize code, follow commit conventions, and manage dependencies across a monorepo. This guide is ideal for contributors aiming for consistency and efficiency in this repository.

## Coding Conventions

### File Naming
- Use **camelCase** for filenames.
  - Example: `physicsEngine.ts`, `sceneManager.ts`

### Import Style
- Use **relative imports** for internal modules.
  - Example:
    ```typescript
    import { PhysicsEngine } from './physicsEngine';
    ```

### Export Style
- Use **named exports** for modules.
  - Example:
    ```typescript
    // In physicsEngine.ts
    export function createWorld() { ... }
    export const GRAVITY = 9.8;
    ```

### Commit Messages
- Follow **conventional commit** format.
- Common prefix: `chore`
  - Example: `chore: update dependencies in packages and apps`
- Average commit message length: ~77 characters.

## Workflows

### Multi-Package Dependency Upgrade
**Trigger:** When you need to update one or more dependencies across multiple packages in the monorepo (often via Dependabot or manually).
**Command:** `/upgrade-dependencies`

1. **Identify outdated dependencies** in each package:
    - Check `apps/*/package.json` and `packages/*/package.json` for outdated versions.
2. **Update the version numbers** in the relevant `package.json` files.
    - Example:
      ```json
      // Before
      "three": "^0.145.0"
      // After
      "three": "^0.146.0"
      ```
3. **Update the root lockfile** (`yarn.lock`) to reflect new dependency versions.
    - Run: `yarn install` or `yarn upgrade`
4. **Commit all changed files** together:
    - Include all updated `package.json` files and `yarn.lock`.
    - Example commit message: `chore: upgrade dependencies across monorepo`
5. **Push and create a pull request** for review.

**Files involved:**
- `apps/*/package.json`
- `packages/*/package.json`
- `yarn.lock`

**Frequency:** ~2-4 times per month

## Testing Patterns

- **Test Framework:** Not explicitly detected.
- **Test File Pattern:** Files named with `.test.` in their filename.
  - Example: `physicsEngine.test.ts`
- **Placement:** Tests are typically placed alongside the modules they test.

**Example Test File:**
```typescript
// physicsEngine.test.ts
import { createWorld } from './physicsEngine';

test('createWorld initializes with default gravity', () => {
  const world = createWorld();
  expect(world.gravity).toBe(9.8);
});
```

## Commands

| Command               | Purpose                                                      |
|-----------------------|--------------------------------------------------------------|
| /upgrade-dependencies | Upgrade dependencies across all packages in the monorepo      |
```
