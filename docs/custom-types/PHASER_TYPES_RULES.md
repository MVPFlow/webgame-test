```
PHASER_TYPES_RULES.md
```

y luego referenciarlo explícitamente desde `docs/AI_RULES.md`.

---

# PHASER + TYPESCRIPT — RULES FOR AI AGENTS

> This file defines **mandatory typing rules** when working with Phaser + TypeScript (strict).
> These rules override convenience or shortcuts.

---

## 1. General rules (MANDATORY)

* ❌ DO NOT create custom typings or shims for Phaser
  (`declare module 'phaser'` is strictly forbidden).
* ✅ ALWAYS rely on official typings shipped with the `phaser` npm package.
* ❌ DO NOT silence TypeScript errors with generic casts unless explicitly allowed below.
* ✅ Prefer **specific Phaser types** over generic ones.

---

## 2. Scene and core objects

* Scenes MUST extend:

```ts
Phaser.Scene
```

* Player, enemies, moving objects with physics MUST be:

```ts
Phaser.Physics.Arcade.Sprite
```

* Simple physical pickups (coins, items) SHOULD be:

```ts
Phaser.Physics.Arcade.Image
```

* Groups with physics MUST be:

```ts
Phaser.Physics.Arcade.Group
```

---

## 3. Arcade Physics callbacks (CRITICAL)

### overlap / collider callbacks

* ❌ DO NOT type callback parameters as `Phaser.GameObjects.GameObject`
* ❌ DO NOT force callback signatures to match manually
* ✅ Let Phaser infer callback types
* ✅ If needed, CAST INSIDE the callback to a **specific Arcade type**

Allowed pattern:

```ts
this.physics.add.overlap(objA, objB, (_a, b) => {
  const target = b as Phaser.Physics.Arcade.Sprite; // or Image
  target.destroy();
});
```

Rules:

* Maximum **ONE cast per callback**
* Cast MUST be to:

  * `Phaser.Physics.Arcade.Sprite`
  * or `Phaser.Physics.Arcade.Image`
* ❌ Never cast to `GameObject` generically

---

## 4. Input typing rules

* `this.input.keyboard` MAY be undefined
* For MVP usage, this is allowed:

```ts
this.input.keyboard!.createCursorKeys();
```

* Using `!` is acceptable
* Optional guards are allowed but not required

---

## 5. children.each rules (IMPORTANT)

* `children.each()` callback MUST return `boolean | null`
* Returning `void` is INVALID

Correct:

```ts
group.children.each((child) => {
  // logic
  return true;
});
```

---

## 6. When TypeScript errors appear

DO:

* Fix the typing at the **usage site**
* Adjust object creation to use correct Arcade types
* Use minimal, explicit casts

DO NOT:

* Create or modify global typings
* Patch errors via fake interfaces
* Relax tsconfig strictness

---

## 7. Priority order when fixing typing issues

1. Use correct Phaser class (Sprite/Image/Group)
2. Let inference work
3. Apply local cast to specific Arcade type
4. Add **one short comment** ONLY if the cast is non-obvious

---

## 8. Enforcement

* All PRs MUST pass:

```bash
npm run typecheck
```

* Any PR introducing:

  * custom Phaser typings
  * global declare modules
  * generic GameObject casts in physics callbacks
    **must be rejected**

---

### End of rules

-------end rules file---------
