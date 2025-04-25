# SvelteKit Routing: Catch-All Routes

In the previous videos, we explored standard and dynamic routes in SvelteKit. This video introduces **Catch-All Routes**, a powerful feature that allows a single route handler to match multiple URL path segments.

## Scenario 6: Documentation Website

Consider building a documentation website with the following potential URL structure:

- `/docs/feature-one/concept-one`
- `/docs/feature-one/concept-two`
- `/docs/feature-two/concept-one`
- ... and so on.

With many features and concepts, this could lead to a large number of individual route files. While dynamic routes for `concept` and `feature` IDs could reduce the file count, managing deeply nested structures for every level of documentation can become cumbersome.

**Catch-All Routes** provide a solution by allowing a single `+page.svelte` file to "catch" all the segments after a specific prefix in the URL.

### Implementation

1.  **Create the `docs` Folder:** Inside the `src/routes` directory, create a new folder named `docs`. This will be the starting point for our documentation routes.

    ```
    src/
    └── routes/
        └── docs/
    ```

2.  **Create the Catch-All Route Folder:** Within the `docs` folder, create a new folder with a special naming convention: `[...slug]`. The three dots `...` before the segment name (`slug` in this case) indicate that this is a catch-all route.

    ```
    src/
    └── routes/
        └── docs/
            └── [...slug]/
    ```

3.  **Create the Page File (`/docs/[...slug]/+page.svelte`):** Inside the `[...slug]` folder, create a `+page.svelte` file.

    ```
    src/
    └── routes/
        └── docs/
            └── [...slug]/
                └── +page.svelte
    ```

4.  **Basic Content for `/docs/[...slug]/+page.svelte` (Initial):**

    ```svelte
    <h1>Docs home page</h1>
    ```

    Now, any URL that starts with `/docs/` will be matched by this single `+page.svelte` file. For example:

    - `/docs/feature-one` will render "Docs home page".
    - `/docs/feature-one/concept-one` will also render "Docs home page".
    - `/docs/feature-two/concept-one/example-a` will also render "Docs home page".

5.  **Accessing the Captured Segments:** To access the individual segments captured by the catch-all route, we use the `page` store from `$app/stores`. The captured segments are available as a string in `page.params.slug`.

    ```svelte
    <script>
      import { page } from '$app/stores';
      console.log($page.params.slug);
    </script>

    <h1>Docs home page</h1>
    ```

    - Visiting `/docs/feature-one` will log `"feature-one"` to the console.
    - Visiting `/docs/feature-one/concept-one` will log `"feature-one/concept-one"`.
    - Visiting `/docs/feature-two/concept-one/example-a` will log `"feature-two/concept-one/example-a"`.

6.  **Processing the Captured Segments:** You can use JavaScript string manipulation (like `.split('/')`) to convert the `slug` string into an array of individual segments for conditional rendering or data fetching.

    ```svelte
    <script>
      import { page } from '$app/stores';
      const slugArray = $page.params.slug ? $page.params.slug.split('/') : [];
    </script>

    {#if slugArray.length === 1}
      <h1>Viewing docs for feature: {slugArray[0]}</h1>
    {:else if slugArray.length === 2}
      <h1>Viewing docs for feature: {slugArray[0]} and concept: {slugArray[1]}</h1>
    {:else}
      <h1>Docs home page</h1>
    {/if}
    ```

    Now:

    - `/docs/routing` will display "Viewing docs for feature: routing".
    - `/docs/routing/catch-all-routes` will display "Viewing docs for feature: routing and concept: catch-all-routes".

## Use Cases for Catch-All Routes

- **Documentation Sites:** As demonstrated, catch-all routes are ideal for handling documentation with varying levels of depth while using a consistent layout.
- **Filtering and Searching:** You can use catch-all routes to capture filter parameters in the URL (e.g., `/products/category/electronics/price/100-500`).
- **Hierarchical Data Display:** For displaying data with multiple levels of categorization.

## Key Takeaway: Catching All Segments

- A folder named `[...segmentName]` within the `routes` directory creates a catch-all route.
- This route will match any URL that starts with the path leading to this folder.
- The captured URL segments after the initial path are available as a string in `page.params.segmentName`.
- You can then process this string to extract individual segments for your application logic.

Catch-all routes provide a flexible way to handle a wide range of URL structures with a single route handler, which can be particularly useful for content-heavy or filter-driven applications.
