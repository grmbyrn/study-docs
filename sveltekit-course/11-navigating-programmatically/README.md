# 🚀 Programmatic Navigation in SvelteKit

In this lesson, we learn how to navigate to different routes **programmatically**—instead of just using anchor (`<a>`) tags.

## 🧠 Why Programmatic Navigation?

Sometimes you need to redirect users **after an event** (like form submission), such as:

- After placing an order → redirect to a confirmation page
- After logging in → go to dashboard

---

## 🛠️ Setup: Adding a Button to Trigger Navigation

**In `+page.svelte` (Home Page):**

```svelte
<script>
  import { goto } from '$app/navigation';

  const handleClick = () => {
    console.log('Placing your order...');

    // Navigate to the products page
    goto('/products');
  }
</script>

<button on:click={handleClick}>Place Order</button>
```

---

## 📦 `goto()` Function

- **Import from** `$app/navigation`
- Syntax:
  ```js
  goto("/target-path", { replaceState: true });
  ```
- `replaceState` (optional):
  - `true`: replaces the current history entry (i.e., doesn't add a new one)
  - `false` (default): adds to browser history stack

---

## 🧪 Example of `replaceState`

```js
goto("/products", { replaceState: true });
```

This prevents the user from returning to the previous route via the browser back button.

---

## 🔁 Navigation Hooks

The `$app/navigation` module also exports **two lifecycle hooks**:

### `beforeNavigate`

- Called **before** navigation occurs
- You can cancel the navigation using `navigation.cancel()`

```js
import { beforeNavigate } from "$app/navigation";

beforeNavigate((navigation) => {
  console.log("Before:", navigation);
  // navigation.from, navigation.to, navigation.type
  // navigation.cancel() - cancels navigation
});
```

---

### `afterNavigate`

- Called **after** navigation has completed

```js
import { afterNavigate } from "$app/navigation";

afterNavigate((navigation) => {
  console.log("After:", navigation);
  // navigation.from, navigation.to, navigation.type
});
```

---

## 🌀 Common Use Cases for Navigation Hooks

- Show/hide loading spinners
- Track analytics
- Guard routes conditionally (e.g., check auth)
- Cancel navigation when form is dirty

---

## ✅ Summary

- Use `goto()` to navigate programmatically in SvelteKit
- Use `{ replaceState: true }` to control browser history
- Use `beforeNavigate` and `afterNavigate` for custom behavior during routing

---
