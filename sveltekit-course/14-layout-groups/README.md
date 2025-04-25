# 🧩 Layout Groups in SvelteKit

## 🎯 Problem:

You want **shared layout** across multiple routes (e.g., `/login`, `/register`) **without** affecting the URL (i.e., avoid `/auth/login`, `/auth/register`).

---

## 🛠️ Use Case: Auth Pages

You want both `/login` and `/register` to share a layout that says:

> **Welcome to Code Evolution**

### ✅ Requirements:

- Shared layout for login & register
- URLs should remain:  
  `/login`  
  `/register`  
  (not `/auth/login`, etc.)

---

## ❌ The Wrong Way: Nested Folder

```bash
src/routes/
├── auth/
│   ├── +layout.svelte    ← defines layout
│   ├── login/
│   │   └── +page.svelte
│   └── register/
│       └── +page.svelte
```

- ✅ Layout works
- ❌ URLs become `/auth/login` and `/auth/register`

---

## ✅ The Right Way: Layout Groups

Use **layout groups** by wrapping the folder name in **parentheses**:

```bash
src/routes/
├── (auth)/
│   ├── +layout.svelte     ← shared layout
│   ├── login/
│   │   └── +page.svelte
│   └── register/
│       └── +page.svelte
```

### 🔍 What This Does:

- Layout in `(auth)/+layout.svelte` applies to all routes inside
- Routes like `/login` and `/register` are still accessible at the same path
- `(auth)` is **not** part of the URL

---

## 📄 Example Code

### `(auth)/+layout.svelte`

```svelte
<h1>Welcome to Code Evolution</h1>
<slot />
```

### `(auth)/login/+page.svelte`

```svelte
<h2>Login</h2>
```

### `(auth)/register/+page.svelte`

```svelte
<h2>Register</h2>
```

---

## 🧪 In the Browser

| URL         | Result                                        |
| ----------- | --------------------------------------------- |
| `/login`    | `Welcome to Code Evolution` + `Login` page    |
| `/register` | `Welcome to Code Evolution` + `Register` page |

---

## 🧠 Key Takeaways

- Layout groups use **folders named in parentheses**: `(group-name)`
- They apply a layout to multiple routes **without** changing the route paths
- Ideal for sections like:
  - Authentication
  - Dashboard
  - Marketing pages
  - Admin interfaces

---
