# SvelteKit Routing: Implementing Nested Routes

In the previous video, we explored the basics of file-based routing in SvelteKit. We learned how `+page.svelte` files within the `routes` folder and its direct subfolders define top-level routes. This video demonstrates how to implement **nested routes** using SvelteKit's intuitive file system structure.

## Scenario 3: Creating Nested Blog Routes

Our goal is to create the following routes for a blog section:

- `/blog`: A general blog landing page.
- `/blog/first`: A specific page for the first blog post.
- `/blog/second`: A specific page for the second blog post.

Let's see how to achieve this using nested folders within the `routes` directory.

### Implementation

1.  **Create the `blog` Folder:** Inside the `src/routes` directory, create a new folder named `blog`. This folder will represent the `/blog` path segment in our URL.

    ```
    src/
    └── routes/
        └── blog/
    ```

2.  **Create the Main Blog Page (`/blog`):** Within the `blog` folder, create a `+page.svelte` file. This file will be rendered when a user navigates to `/blog`.

    ```
    src/
    └── routes/
        └── blog/
            └── +page.svelte
    ```

3.  **Add Content to `/blog/+page.svelte`:**

    ```svelte
    <h1>My blog</h1>
    ```

    Now, running `npm run dev` and navigating to `http://localhost:5173/blog` will display "My blog".

4.  **Create Nested Folders for Blog Posts:** To create the `/blog/first` and `/blog/second` routes, create two new folders, `first` and `second`, inside the `src/routes/blog` folder.

    ```
    src/
    └── routes/
        └── blog/
            ├── first/
            └── second/
    ```

5.  **Create `+page.svelte` Files in Nested Folders:** Inside each of the `first` and `second` folders, create a `+page.svelte` file.

    ```
    src/
    └── routes/
        └── blog/
            ├── first/
            │   └── +page.svelte
            └── second/
                └── +page.svelte
    ```

6.  **Add Content to the Nested `+page.svelte` Files:**

    - `src/routes/blog/first/+page.svelte`:

      ```svelte
      <h1>First blog post</h1>
      ```

    - `src/routes/blog/second/+page.svelte`:

      ```svelte
      <h1>Second blog post</h1>
      ```

Now, when you navigate to:

- `http://localhost:5173/blog/first`, you will see "First blog post".
- `http://localhost:5173/blog/second`, you will see "Second blog post".

The main `/blog` route will still display "My blog".

## Key Takeaway: Nested Folders for Nested Routes

SvelteKit's file-based routing makes implementing nested routes incredibly straightforward. By simply nesting folders within the `src/routes` directory, the URL structure automatically mirrors your folder hierarchy. Each `+page.svelte` file within these nested folders becomes accessible at the corresponding nested URL path.

In the upcoming video, we will explore another powerful routing feature: **Dynamic Routes**. Stay tuned!
