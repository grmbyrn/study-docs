# Understanding the SvelteKit Project Structure

This document provides an overview of the files and folders generated in a basic SvelteKit application, as explained in the accompanying video tutorial. Understanding this structure is crucial for navigating and developing your SvelteKit projects effectively.

When you create a new SvelteKit project, you'll find a set of core files and folders at the root level (excluding the `.vscode` folder if you have it open in VS Code). Let's explore these:

## Root Level Files

- **`package.json`:** This file is the heart of your Node.js project. It contains:

  - **`dependencies`:** Lists the packages your project relies on, including `svelte`, `sveltekit`, `vite`, `eslint`, and `prettier`. As of the video, `sveltekit` version is `1.0.0`, but newer versions are likely. The core concepts remain consistent.
  - **`scripts`:** Defines various commands you can run using `npm run <script-name>`. The essential scripts include:
    - `dev`: Starts the SvelteKit application in development mode with hot reloading.
    - `build`: Compiles your SvelteKit application for production deployment.
    - `preview`: Starts the built application in production mode (requires running `build` first).
    - `lint`: Analyzes your code for potential issues using ESLint.
    - `format`: Automatically formats your code using Prettier.
  - **`type: "module"`:** This indicates that `.js` files in your project are treated as native JavaScript modules, allowing the use of `import` and `export` syntax.

- **`package-lock.json`:** This file ensures consistent installation of your project's dependencies across different environments. You generally don't need to interact with this file directly.

- **`.gitignore`:** Specifies files and directories that should be ignored by Git for version control (e.g., `node_modules`, `.svelte-kit`).

- **`.npmrc`:** This file can contain npm configuration settings. The video mentions `engine-strict` which enforces Node.js and npm version compatibility.

- **`README.md`:** Contains basic instructions for running, building, and deploying the application. We are currently reading this file!

- **`svelte.config.js`:** This is the main SvelteKit configuration file. It exports a `config` object used by SvelteKit and other integrating tools. The video briefly mentions the `adapter` configuration, which is used for generating output for different deployment environments. As a beginner, you likely won't need to modify this immediately.

- **`vite.config.js`:** SvelteKit internally uses Vite as its build tool. This file is the Vite configuration file. A SvelteKit project is essentially a Vite project utilizing the `@sveltejs/vite-plugin-svelte` plugin, along with other Vite plugins you can configure here.

- **`.eslintrc.cjs`:** This is the configuration file for ESLint. It extends recommended ESLint rules and adds Svelte as a plugin for Svelte-specific linting.

- **`.eslintignore`:** Lists files and directories that ESLint should ignore during the linting process.

- **`.prettierrc.cjs`:** This is Prettier's configuration file, defining code formatting rules.

- **`.prettierignore`:** Contains a list of files that Prettier should ignore during code formatting.

## Project Folders

- **`.svelte-kit`:** This folder is automatically generated when you run the `dev` or `build` scripts. It contains the built output and other internal files used by SvelteKit to serve your application. This folder is typically Git-ignored.

- **`node_modules`:** This folder houses all the npm packages (dependencies) that your project relies on. It is generated when you run `npm install` and is also Git-ignored.

- **`static`:** This folder is for static assets that should be served directly without any processing. Examples include `favicon.png`, `robots.txt`, and other images or files.

- **`src`:** This is the most important folder where the main source code of your SvelteKit application resides. It contains:
  - **`routes`:** This folder is the foundation of SvelteKit's routing system. Each file and folder within `routes` defines a specific route in your application. For instance, `+page.svelte` at the root of the `routes` directory is the file that gets rendered when you visit the root path (`/`) of your application (e.g., `http://localhost:5173`). This is the file you modified in the previous video.
  - **`app.html`:** This file serves as the main HTML template for your application. It contains placeholders:
    - `%sveltekit.assets%`: Points to the static assets in the `static` folder.
    - `%sveltekit.head%`: Used for injecting `<link>` and `<script>` elements required by your app.
    - `%sveltekit.body%`: This placeholder is where the content from your SvelteKit pages (like `+page.svelte`) is injected and rendered in the final HTML.

When you visit a specific route in your SvelteKit application, the corresponding file in the `src/routes` directory is rendered, and its content replaces the `%sveltekit.body%` placeholder in `app.html` to form the final HTML document displayed in the browser.

Understanding this basic project structure is the first step towards building more complex and feature-rich SvelteKit applications.
