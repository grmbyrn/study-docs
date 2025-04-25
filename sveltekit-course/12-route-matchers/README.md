# 🔍 Route Matchers in SvelteKit

Dynamic routes in SvelteKit (e.g. `/products/[productId]`) can match **any value**—including unwanted strings like `/products/batman`.

To restrict which values match a dynamic segment, **route matchers** can be used.

---

## 🧠 What Is a Route Matcher?

A **route matcher** is a function that evaluates a route parameter and returns:

- `true` → valid match
- `false` → invalid match (results in a 404)

---

## 🎯 Use Case

Restrict `/products/[productId]` to accept only **numeric IDs**, e.g.:

- ✅ `/products/1`
- ✅ `/products/100`
- ❌ `/products/batman`

---

## 🛠️ Step-by-Step: Creating a Route Matcher

### ✅ Step 1: Create a Matcher Function

1. Inside your `src` directory, create a folder:

```bash
src/params/
```

2. Add a file named `integer.js`:

```js
// src/params/integer.js
export function match(param) {
  return /^\d+$/.test(param); // only allow digits
}
```

> 🧠 The function **must** be named `match` – this is a SvelteKit convention.

---

### ✅ Step 2: Apply Matcher to the Route

Rename your route folder or file to:

```
src/routes/products/[productId=integer]/
```

This links the `[productId]` parameter to your custom `integer` matcher.

---

## 🧪 Test the Behavior

| Route              | Result           |
| ------------------ | ---------------- |
| `/products/1`      | ✅ Page shows    |
| `/products/100`    | ✅ Page shows    |
| `/products/batman` | ❌ 404 Not Found |

---

## ✅ Benefits

- Improves route precision
- Avoids invalid routes
- Prevents users or crawlers from accessing unintended URLs

---

## 📝 Summary

- Matchers are custom functions that determine if a route parameter is valid
- Create them in `src/params/`
- Must export a `match()` function
- Add matcher name to route parameter: `[param=matcherName]`

---
