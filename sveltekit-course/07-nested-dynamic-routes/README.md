# SvelteKit Routing: Nested Dynamic Route Segments

In the previous video, we explored how to create dynamic routes using bracketed folder names. This video builds upon that knowledge to demonstrate how to implement **nested dynamic routes**, allowing for multiple dynamic segments within a single URL path.

## Scenario 5: Product Details with Nested Reviews

Consider a scenario where we need to display product details and then the reviews for a specific product:

- `/products/[productId]`: Displays details for a product with a given ID (e.g., `/products/1`).
- `/products/[productId]/reviews/[reviewId]`: Displays a specific review for a specific product (e.g., `/products/1/reviews/1`).

Let's see how to achieve this using nested dynamic route segments in SvelteKit.

### Implementation

1.  **Existing Product ID Route:** We already have the dynamic `[productId]` route set up within the `src/routes/products` folder from the previous video:

    ```
    src/
    └── routes/
        └── products/
            └── [productId]/
                └── +page.svelte
    ```

2.  **Nest the `reviews` Folder:** To create the `/reviews` segment under a specific product, create a new folder named `reviews` inside the `[productId]` folder.

    ```
    src/
    └── routes/
        └── products/
            └── [productId]/
                └── reviews/
    ```

3.  **Create the Dynamic `[reviewId]` Folder:** Within the `reviews` folder, create another folder with a dynamic segment: `[reviewId]`.

    ```
    src/
    └── routes/
        └── products/
            └── [productId]/
                └── reviews/
                    └── [reviewId]/
    ```

4.  **Create the Review Page (`/products/[productId]/reviews/[reviewId]/+page.svelte`):** Inside the `[reviewId]` folder, create a `+page.svelte` file.

    ```
    src/
    └── routes/
        └── products/
            └── [productId]/
                └── reviews/
                    └── [reviewId]/
                        └── +page.svelte
    ```

5.  **Access Both Dynamic Parameters:** In the `+page.svelte` file, import the `page` store and extract both the `productId` and the `reviewId` from the `page.params` object:

    ```svelte
    <script>
      import { page } from '$app/stores';
      const productId = $page.params.productId;
      const reviewId = $page.params.reviewId;
    </script>

    <h1>Review {$reviewId} for product {$productId}</h1>
    ```

Now, when you navigate to:

- `http://localhost:5173/products/1/reviews/1`, you will see "Review 1 for product 1".
- `http://localhost:5173/products/100/reviews/5`, you will see "Review 5 for product 100".

## Key Takeaway: Nesting Dynamic Segments

SvelteKit allows you to nest dynamic route segments by creating bracketed folders within other folders, including other dynamic segment folders. The URL structure directly reflects this nested folder hierarchy. You can access all the dynamic parameters in the corresponding `+page.svelte` file through the `page.params` object, with keys matching the names you gave to your dynamic segments in the folder structure.

This feature enables you to build complex and deeply nested URL structures to represent intricate data relationships within your application.

In the next video, we will explore another SvelteKit feature for handling multiple dynamic path segments in a different way. Stay tuned!
