# SvelteKit Routing: File System Based Approach

This document explains SvelteKit's file system-based routing mechanism, where the structure of files and folders within your project directly defines the URL paths accessible in the browser.

## File System Routing in SvelteKit

SvelteKit adopts a convention-over-configuration approach to routing. This means that the framework automatically creates routes based on the organization of your files within a specific directory.

### Key Routing Conventions

1.  **The `routes` Folder:** All route-related files and folders **must** reside within a folder named `routes` located in the `src` directory of your SvelteKit project.

2.  **`+page.svelte` for Page Components:** Every file that corresponds to a routable page in the browser **must** be named `+page.svelte`. The `+page` part signifies that this Svelte component should be rendered when the associated URL path is accessed.

3.  **Folders as Path Segments:** Each folder created directly under the `routes` directory (or nested within it) represents a segment in the browser URL path.

When you adhere to these conventions, SvelteKit automatically makes the corresponding `+page.svelte` file accessible as a route. There's no need for manual router installation or configuration.

## Scenario 1: The Home Page (`/`)

To create a route that renders when a user visits the root of your website (`http://localhost:5173` by default during development), you need to:

1.  **Create a `routes` folder** inside your `src` directory if it doesn't already exist.

    ```
    src/
    └── routes/
    ```

2.  **Create a `+page.svelte` file** directly within the `routes` folder.

    ```
    src/
    └── routes/
        └── +page.svelte
    ```

3.  **Add your HTML content** to `+page.svelte`. For example:

    ```svelte
    <h1>Welcome home</h1>
    ```

When you run your SvelteKit development server (`npm run dev`), navigating to `http://localhost:5173` in your browser will render the content of this `+page.svelte` file.

## Scenario 2: About (`/about`) and Profile (`/profile`) Pages

To create routes for `/about` and `/profile` pages:

1.  **Create folders** named `about` and `profile` inside the `routes` folder. The folder names will become the path segments in the URL.

    ```
    src/
    └── routes/
        ├── about/
        └── profile/
    ```

2.  **Create a `+page.svelte` file** inside each of these new folders.

    ```
    src/
    └── routes/
        ├── about/
        │   └── +page.svelte
        └── profile/
            └── +page.svelte
    ```

3.  **Add the respective content** to each `+page.svelte` file:

    - `src/routes/about/+page.svelte`:

      ```svelte
      <h1>About me</h1>
      ```

    - `src/routes/profile/+page.svelte`:

      ```svelte
      <h1>My profile</h1>
      ```

Now, when you run your development server:

- Visiting `http://localhost:5173/about` will render the "About me" content.
- Visiting `http://localhost:5173/profile` will render the "My profile" content.
- The root URL (`http://localhost:5173/`) will still render the "Welcome home" content from the `src/routes/+page.svelte` file.

## Handling Non-Matching Routes (404)

SvelteKit automatically handles cases where a user navigates to a URL that doesn't map to any file structure within your `routes` folder. In such scenarios, SvelteKit will respond with a standard **404 Not Found** error page without requiring any explicit configuration on your part.

## Convention over Configuration

As demonstrated, SvelteKit's routing is heavily based on convention. The structure of your files and folders within the `src/routes` directory dictates the available URL paths. This approach eliminates the need for manual router setup and configuration, making it intuitive and straightforward to define your application's navigation.

There's much more to explore about routing in SvelteKit, including dynamic routes, layout routes, and more. Stay tuned for the next video to delve deeper into these advanced routing features!
