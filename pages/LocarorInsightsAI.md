# 🧠 Selector Strategy – Best Practices (Playwright / TypeScript)

This document describes a **production-grade selector strategy** used in real-world Playwright + TypeScript projects.

The goal is to create selectors that are:

* stable
* readable
* maintainable
* resilient to UI, CSS, and localization changes

---

## 🎯 Main Goal

A selector should **survive the longest** when:

* UI changes
* CSS or layout is refactored
* the framework version changes
* the application is localized (i18n)

> **A good selector describes what the element does, not how it looks.**

---

## 🏆 Golden Rule

### Locator ≠ Assertion

* **Locator** → how we find the element
* **Assertion** → what we verify about it

Avoid mixing the two unless absolutely necessary.

---

## 🥇 Selector Priority Ladder (Used in Real Projects)

### 1️⃣ `data-testid` / `data-test`

```ts
page.getByTestId('dialog-link');
```

**Use when:**

* regression tests
* critical user flows
* CI pipelines

**Why:**

* explicit contract between Dev & QA
* unaffected by styling or copy changes
* most stable option

---

### 2️⃣ Stable `id` (Non-framework)

```ts
page.locator('#dialog-link');
```

✔ very stable
❌ often unavailable

---

### 3️⃣ Tag + Business Attribute (Most Common Pro Choice)

```ts
page.locator('a[href*="/modal-overlays/dialog"]');
```

**Business attributes include:**

* `href`
* `name`
* `value`
* `type`
* `aria-*`

These attributes represent **application behavior**, not styling.

---

### 4️⃣ `getByRole()` (Accessibility-based)

```ts
page.getByRole('link', { name: 'Dialog' });
```

**Good for:**

* smoke tests
* accessibility tests
* when no better attribute exists

⚠ Still depends on visible text → fragile with localization.

---

### 5️⃣ Structural / Scoped Selectors

```ts
menu.locator('li').nth(2).locator('a');
```

Use **only if the DOM structure is guaranteed to be stable**.

---

### 6️⃣ Text-only Selectors (Last Resort)

```ts
page.getByText('Dialog');
```

❌ fragile
❌ localization-unfriendly
❌ mixes locator and assertion

---

### ❌ Avoid in Regression Tests

* framework-generated classes (`ng-*`, `css-*`)
* full class strings
* XPath

---

## 🧭 Selector Decision Tree (5-second rule)

```text
1. Is there a data-testid?
   → Use it

2. Is there a business attribute (href, name, value)?
   → Use tag + attribute

3. Is there a reliable ARIA role?
   → Use getByRole()

4. Only text is available?
   → Use only for smoke tests
```

---

## 🧱 Page Object Architecture (Real-World Example)

### Page Object (Selectors only)

```ts
export class NavigationPage {
  constructor(private page: Page) {}

  dialogLink(): Locator {
    return this.page.locator(
      'a[href*="/modal-overlays/dialog"]'
    );
  }
}
```

### Test (Assertions only)

```ts
await expect(nav.dialogLink()).toBeVisible();
await expect(nav.dialogLink()).toHaveText('Dialog');
```

✔ clear responsibility
✔ easy debugging
✔ easy maintenance

---

## 🧪 Always Use Strict Mode

```ts
await expect(nav.dialogLink()).toHaveCount(1);
```

Fail fast → detect bad selectors early.

---

## 🌍 Localization (i18n) Safe Strategy

### ❌ Avoid

```ts
getByText('Dialog');
```

### ✅ Prefer

```ts
a[href*="/modal-overlays/dialog"];
```

or

```ts
page.getByTestId('nav-dialog');
```

---

## 🧩 Fallback Selector Strategy (Production-grade)

```ts
dialogLink(): Locator {
  return this.page
    .locator('a[href*="/modal-overlays/dialog"]')
    .or(this.page.getByRole('link', { name: 'Dialog' }));
}
```

Stable + readable.

---

## 🏁 TL;DR

* Locator ≠ Assertion
* Attributes > Text
* `href` represents business intent
* Partial match > exact match
* Page Objects contain selectors
* Tests contain expectations

---

This strategy reflects **enterprise-level Playwright usage** and is suitable for long-term maintenance in large-scale test suites.
