Here's a clean set of **SvelteKit notes** based on the video covering **special files, regular components, and lib folder usage**:

---

# 📁 Special vs. Regular Files in SvelteKit

## ✅ Special Files

SvelteKit recognizes certain **special files** in the `routes` folder that **map to routes** automatically:

- `+page.svelte` → Maps to a route's main page
- `+layout.svelte` → Defines a layout for that route and children

> These are tied directly to **routing behavior**

---

## 🧩 Regular Components in `routes/`

What happens when you create **regular Svelte components** (e.g., `Header.svelte`, `Footer.svelte`) in the `routes/` folder?

### 💡 Answer:

- They **don’t** create a route.
- They are treated as **internal components**, just like components anywhere else.
- You **won’t** be able to visit `/header` or `/footer`.

---

## 🛠️ Practical Example: Extracting Layout Parts

Let's say you have this in `+layout.svelte`:

```svelte
<!-- Old layout -->
<header class="layout-header">...</header>
<slot />
<footer class="layout-footer">...</footer>
```

### 🔄 Step 1: Create Regular Components

📄 `src/routes/Header.svelte`  
📄 `src/routes/Footer.svelte`

Move the HTML and CSS for header and footer into them.

### 🔄 Step 2: Use in `+layout.svelte`

```svelte
<script>
  import Header from './Header.svelte';
  import Footer from './Footer.svelte';
</script>

<Header />
<slot />
<Footer />
```

✅ UI still works.  
❌ Still no new routes are created.

---

## 🗂️ When to Use the `lib/` Folder

SvelteKit allows you to place **shared code** in the `src/lib` folder.

### 🔥 Benefits:

- Meant for **reusable components, stores, utils, API helpers, etc.**
- Can be imported using `@` or `$lib` aliases
- Keeps `routes/` clean and focused on routing

---

### 💡 Moving Components to `lib`

📁 `src/lib/Header.svelte`  
📁 `src/lib/Footer.svelte`

Then in your layout:

```svelte
<script>
  import Header from '$lib/Header.svelte';
  import Footer from '$lib/Footer.svelte';
</script>

<Header />
<slot />
<Footer />
```

✅ Cleaner path imports  
✅ Better project organization  
✅ Reusable across the app

---

## 🧠 Summary

| Concept                      | Behavior                     |
| ---------------------------- | ---------------------------- |
| `+page.svelte`               | Maps to a URL route          |
| `+layout.svelte`             | Wraps routes under it        |
| `Header.svelte` in `routes/` | Does NOT create a route      |
| `lib/` folder                | For shared, reusable logic   |
| `$lib/Component`             | Path alias for clean imports |

---

Let me know if you want a diagram or folder layout image for this!
