# 🧱 Layouts in SvelteKit

So far, we've treated each page as an independent component. On navigation, the current page is destroyed and a new one is rendered. But real-world apps usually have a **persistent layout**, like a header and footer shared across all pages.

SvelteKit makes this easy using layout components.

---

## 🎯 Why Use Layouts?

- Add persistent elements (e.g. header, footer)
- Avoid repeating markup/styles in every page
- Enable **nested layouts** for different sections

---

## 📁 Step 1: Create a Root Layout

In your `src/routes/` directory, create a file:

```bash
+layout.svelte
```

Inside it:

```svelte
<script>
  // Optional script logic
</script>

<header class="layout-header">This is the header</header>

<slot /> <!-- This is where page content will be rendered -->

<footer class="layout-footer">This is the footer</footer>

<style>
  .layout-header, .layout-footer {
    background-color: #333;
    color: white;
    font-size: 1.2rem;
    text-align: center;
    padding: 10px;
  }
</style>
```

### 🧠 Notes:

- The `<slot />` tag is **required** — it renders the page content.
- This layout will now wrap **all pages** in your app (e.g. `/`, `/blog`, `/products`).

---

## 🧩 Step 2: Create a Nested Layout (Optional)

You can add layouts to specific sections of your app, like product detail pages.

Example folder structure:

```
src/routes/products/[productId]/+layout.svelte
```

In `+layout.svelte`:

```svelte
<h3>Featured Products</h3>
<slot />
```

Now, every route like `/products/1` or `/products/42` will include this layout **in addition to** the root layout.

---

## 🧪 Navigation Behavior

| Route           | Layouts Applied             |
| --------------- | --------------------------- |
| `/`             | Root layout                 |
| `/products`     | Root layout                 |
| `/products/1`   | Root + `[productId]` layout |
| `/products/100` | Root + `[productId]` layout |

---

## ✅ Summary

- **Root layout**: `+layout.svelte` in `routes/` applies to the entire app.
- **Nested layout**: `+layout.svelte` in subfolders applies to specific routes.
- Use `<slot />` in layout components to render child content.
- Great for headers, sidebars, footers, or context setup (like loading states or authentication guards).

---
