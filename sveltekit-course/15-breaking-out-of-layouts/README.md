# 🛑 Breaking Out of Layouts in SvelteKit

## 🎯 Objective:

## Override SvelteKit's **default layout inheritance** and **opt-out** of layouts selectively for certain pages.

## 🧱 Project Structure Example

```
src/routes/
├── +layout.svelte         ← Root layout (e.g., header/footer)
├── (auth)/                ← Auth layout group
│   ├── +layout.svelte     ← Auth layout
│   └── password/
│       ├── +layout.svelte ← Password layout
│       ├── info/+page.svelte
│       ├── forgot/+page.svelte
│       └── reset/+page.svelte
```

---

## 🧪 Default Behavior

Every route **inherits layouts** from:

1. Root (`+layout.svelte`)
2. Group (`(auth)/+layout.svelte`)
3. Nested folder (`password/+layout.svelte`)

### Example:

URL: `/password/info`

- Renders:
  - Root layout
  - Auth layout
  - Password layout
  - Info page content ✅

---

## 🧯 Breaking Layout Inheritance

SvelteKit allows us to **skip** one or more layouts via **special file names**:

### 🔓 Syntax:

Rename `+page.svelte` to:

```
+page@layout.svelte     → skips layout of folder `layout`
+page@.svelte           → skips all layouts except root
```

> Note: This applies to `+layout.svelte` files too!

---

### 🧪 Example 1: Skip Password Layout

📄 `forgot/+page@auth.svelte`

- ✅ Uses:
  - Root layout
  - Auth layout
- ❌ Skips:
  - Password layout

### 🧪 Example 2: Skip Auth + Password Layout

📄 `reset/+page@.svelte`

- ✅ Uses:
  - Root layout only
- ❌ Skips:
  - Auth layout
  - Password layout

---

## 🧪 Visual Confirmation (Browser Behavior)

| Route              | Layouts Used                    |
| ------------------ | ------------------------------- |
| `/password/info`   | Root → Auth → Password ✅       |
| `/password/forgot` | Root → Auth ❌ Password skipped |
| `/password/reset`  | Root only ❌ Auth ❌ Password   |

---

## ✨ BONUS: Breaking Layout from a Layout

This trick works on `+layout.svelte` too!

> 📄 Rename: `+layout@.svelte`  
> Result: That layout will not inherit from parent layouts.

🧪 **Exercise Idea:**

- Try renaming `password/+layout.svelte` to `+layout@.svelte`
- Refresh `/password/info`
- Observe: The Password layout is now **self-contained**, without `auth` or root layouts.

---

## 🧠 Summary

- Use **`@segment`** to **opt out** of specific layout inheritance
- Use **`@.svelte`** to break **all the way to root layout**
- Works for both **pages** and **layouts**
- Great for flexibility when you want different layout behavior across pages

---
