# SvelteKit Routing: Dynamic Route Segments

In the previous video, we explored nested routes. While useful for hierarchical content, defining routes based on predefined paths isn't always scalable for applications dealing with dynamic data. This video introduces **Dynamic Route Segments** in SvelteKit, allowing you to create routes that can handle a range of values in a specific part of the URL.

## Scenario 4: Product Listing and Detail Pages

Our goal is to create routes for a product listing and individual product detail pages:

- `/products`: Displays a list of products.
- `/products/[productId]`: Displays details for a specific product, where `[productId]` can be any product identifier (e.g., `/products/1`, `/products/2`, `/products/abc`).

### Implementation

1.  **Create the `products` Folder:** Inside the `src/routes` directory, create a new folder named `products`.

    ```
    src/
    └── routes/
        └── products/
    ```

2.  **Create the Product Listing Page (`/products`):** Within the `products` folder, create a `+page.svelte` file to display the list of products.

    ```
    src/
    └── routes/
        └── products/
            └── +page.svelte
    ```

3.  **Add Content to `/products/+page.svelte`:**

    ```svelte
    <h1>Product List</h1>
    <ul>
      <li>Product 1</li>
      <li>Product 2</li>
      <li>Product 3</li>
    </ul>
    ```

    Navigating to `http://localhost:5173/products` will now show the product list.

4.  **Create the Dynamic Route Folder:** Inside the `products` folder, create a new folder with a special naming convention: `[productId]`. The square brackets indicate that `productId` is a **dynamic route segment**.

    ```
    src/
    └── routes/
        └── products/
            └── [productId]/
    ```

5.  **Create the Product Detail Page (`/products/[productId]`):** Within the `[productId]` folder, create a `+page.svelte` file.

    ```
    src/
    └── routes/
        └── products/
            └── [productId]/
                └── +page.svelte
    ```

6.  **Basic Content for `/products/[productId]/+page.svelte` (Initial):**

    ```svelte
    <h1>Details about product</h1>
    ```

    Now, navigating to URLs like `http://localhost:5173/products/1`, `http://localhost:5173/products/2`, or even `http://localhost:5173/products/abc` will all render this basic product details page. SvelteKit treats the `[productId]` segment as a dynamic placeholder.

## Accessing Route Parameters

To display the specific `productId` in our detail page, we need to access the route parameter. SvelteKit provides the `@sveltejs/kit` `stores` module for this purpose.

1.  **Import the `page` Store:** Add a `<script>` block at the top of your `src/routes/products/[productId]/+page.svelte` file and import the `page` store:

    ```svelte
    <script>
      import { page } from '$app/stores';
      // '$app/stores' provides various stores related to the application state.
    </script>
    ```

2.  **Access the Dynamic Parameter:** The `page` store is a readable store whose `value` contains information about the current page, including route parameters. These parameters are available within the `page.params` object. The keys in `page.params` correspond to the names you gave your dynamic route segments (in this case, `productId`). We can access the `productId` like this:

        ```javascript
        <script>
          import { page } from '$app/stores';
          const productId = <span class="math-inline">page\.params\.productId;

    // The '</span>' prefix is Svelte's auto-subscription syntax for stores.
    </script>
    ```

3.  **Display the Product ID:** Update the HTML in your `+page.svelte` file to display the `productId`:

    ```svelte
    <script>
      import { page } from '$app/stores';
      const productId = $page.params.productId;
    </script>

    <h1>Details about product {$productId}</h1>
    ```

Now, when you navigate to:

- `http://localhost:5173/products/1`, you will see "Details about product 1".
- `http://localhost:5173/products/100`, you will see "Details about product 100".
- `http://localhost:5173/products/my-item`, you will see "Details about product my-item".

## Key Takeaways: Dynamic Routes

- Wrapping a folder name in square brackets (e.g., `[folderName]`) creates a **dynamic route segment**.
- SvelteKit maps any value in that URL segment to the dynamic parameter.
- You can access these dynamic parameters within your `+page.svelte` file using the `page` store from `$app/stores`. The parameters are available in the `page.params` object, with keys matching the names you gave to your dynamic segments.

Dynamic routes are essential for building applications that display information based on unique identifiers, such as product IDs, user IDs, or article slugs, following the common list-detail pattern.
