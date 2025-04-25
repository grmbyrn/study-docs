Markdown

# SvelteKit Routing: Navigating with UI Elements

In the previous videos, we've explored various aspects of SvelteKit's file-based routing. However, we've primarily navigated by manually entering URLs in the browser. This video demonstrates how to navigate between routes using standard HTML anchor (`<a>`) elements within your SvelteKit application's UI.

## Example 1: Navigating from Home to Blog

To navigate from the homepage (`/`) to the `/blog` page, you can simply use an anchor tag in your `src/routes/+page.svelte` file:

```svelte
<a href="/blog">Blog</a>
```

When this link is clicked in the browser, SvelteKit will handle the navigation to the /blog route.

## Example 2: Navigating to the Products Page

Similarly, to add a link to the /products page on your homepage, add another anchor tag:

```Svelte

<a href="/blog">Blog</a>
<a href="/products">Products</a>
```

Clicking the "Products" link will navigate the user to the /products route.

## Example 3: Navigating Back to Home

To create a link on the `/products` page `(src/routes/products/+page.svelte)` that navigates back to the homepage, use an anchor tag with the root path `(/)` as the href:

```Svelte

<h1>Product List</h1>
<ul>
  <li><a href="/products/1">Product 1</a></li>
  <li><a href="/products/2">Product 2</a></li>
  <li><a href="/products/3">Product 3</a></li>
</ul>
<a href="/">Home</a>
```

Clicking the `Home` link will take the user back to the root of your application.

## Example 4: Navigating to Dynamic Routes

To navigate to dynamic routes, you construct the href attribute with the dynamic segment included. For our product details page (`/products/[productId]`), we can modify the product list on the `/products` page (`src/routes/products/+page.svelte`) to include links to individual product details:

```Svelte
<h1>Product List</h1>
<ul>
  <li><a href="/products/1">Product 1</a></li>
  <li><a href="/products/2">Product 2</a></li>
  <li><a href="/products/3">Product 3</a></li>
</ul>
<a href="/">Home</a>
```

Clicking on `Product 1`, `Product 2`, or `Product 3` will navigate to the corresponding dynamic product detail routes (`/products/1`, `/products/2`, `/products/3`).

Generating Dynamic Links with Props
Often, the dynamic segment value might be passed as a prop to your component. Let's simulate this by defining a productId prop in our src/routes/products/+page.svelte file (although we are not explicitly passing it in this example):

```Svelte
<script>
  export let productId = 100; // Assume productId is passed as a prop
</script>

<h1>Product List</h1>
<ul>
  <li><a href="/products/1">Product 1</a></li>
  <li><a href="/products/2">Product 2</a></li>
  <li><a href="/products/3">Product 3</a></li>
</ul>
<a href="/">Home</a>
<a href={`/products/${productId}`}>Product {productId}</a>
```

Here, we use template literals (backticks) to dynamically construct the href attribute using the `productId` prop. Clicking the "Product 100" link will navigate to `/products/100`.

### Key Takeaway: Using Anchor Elements for Navigation

SvelteKit leverages standard HTML anchor (`<a>`) elements for navigating between routes within your application. You simply set the `href` attribute of the `<a>` tag to the desired URL path. For dynamic routes, you construct the `href` with the appropriate dynamic segment values, often using string interpolation or template literals when the dynamic data is available in your component.
