# Your First SvelteKit Application

This guide walks you through the initial steps of creating your very first SvelteKit application, based on the accompanying video tutorial.

## Prerequisites

Before you begin, ensure you have the following installed on your system:

1.  **Node.js:** SvelteKit requires Node.js. You can download and install the latest stable release from the official website: [https://nodejs.org/](https://nodejs.org/). If you already have Node.js installed, it's a good practice to update it to the latest version.

2.  **Text Editor:** While you can use any text editor, **Visual Studio Code (VS Code)** is highly recommended for SvelteKit development due to its excellent features and extensions. You can download and install it from: [https://code.visualstudio.com/](https://code.visualstudio.com/).

## Setting Up Your Workspace

1.  **Create a Project Folder:** Open your terminal or command prompt and create a new folder where your SvelteKit project will reside. In the video, a folder named `sweltkit` was created.

    ```bash
    mkdir sweltkit
    cd sweltkit
    ```

2.  **Open in VS Code (Optional but Recommended):** Open the newly created folder in Visual Studio Code. You can do this by navigating to the folder in your file explorer and right-clicking to select "Open with Code" or by opening VS Code and then selecting "File" > "Open Folder...".

## Creating Your SvelteKit Project

1.  **Open the Terminal in VS Code:** Inside VS Code, open the integrated terminal by pressing `Ctrl + Backtick` (`` Ctrl + `  ``) on Windows/Linux or `Cmd + Backtick` (`` Cmd + `  ``) on macOS.

2.  **Run the Create SvelteKit Command:** In the terminal, run the following command to create a new SvelteKit project:

    ```bash
    npm create svelte@latest hello-world
    ```

    Here, `hello-world` is the name you're giving to your project folder. You can choose a different name if you prefer.

3.  **Interactive CLI Prompts:** The command will initiate an interactive command-line interface (CLI) with a series of questions:

    - **Choose a template:** Select **Skeleton project**. This provides a bare-bones scaffolding for a new SvelteKit application.

    - **Add types to the project?** Select **No**. This guide will proceed without TypeScript.

    - **Add ESLint for code linting?** Select **Yes**. ESLint helps identify and fix code style issues.

    - **Add Prettier for code formatting?** Select **Yes**. Prettier automatically formats your code for consistency.

    - **Add Playwright for browser testing?** Select **No**. Browser testing will not be covered in this initial setup.

    - **Add Vitest for unit testing?** Select **No**. Unit testing will also not be covered in this initial setup.

4.  **Project Creation:** Once you've answered all the questions, the CLI will create a new folder named `hello-world` (or whatever name you chose) containing the basic structure of your SvelteKit application.

## Running Your SvelteKit Application

The terminal will provide instructions on the next steps. Typically, these are:

1.  **Navigate to the Project Folder:**

    ```bash
    cd hello-world
    ```

2.  **Install Dependencies:** Install the necessary Node.js packages by running:

    ```bash
    npm install
    ```

3.  **Initialize Git (Optional but Recommended):** If you are familiar with Git for version control, initialize it in your project:

    ```bash
    git init
    ```

4.  **Start the Development Server and Open in Browser:** Run the following command to start the development server and automatically open your application in your default web browser:

    ```bash
    npm run dev -- --open
    ```

    This command will typically open your application at `http://localhost:5173`. You should see a default SvelteKit welcome page with the heading "Welcome to SvelteKit" and a link to the documentation.

## Making Your First Change

1.  **Open Project in VS Code (If Not Already Open):** Open the `hello-world` folder in VS Code.

2.  **Navigate to the Main Page File:** In the VS Code explorer, navigate to the `src` folder, then the `routes` folder, and finally open the `+page.svelte` file.

3.  **Edit the Content:** Locate the `<h1>` tag within the `<script>` and `<svelte:head>` sections and the main HTML content. Replace the text "Welcome to SvelteKit" with "Hello World":

    ```svelte
    <script>
      import { dev } from '$app/environment';
    </script>

    <svelte:head>
      <title>Home</title>
    </svelte:head>

    <h1>Hello World</h1>

    <p>visit <a href="[https://kit.svelte.dev](https://kit.svelte.dev)">kit.svelte.dev</a> to learn more</p>
    ```

4.  **Save the Changes:** Save the `+page.svelte` file (`Ctrl + S` or `Cmd + S`).

5.  **Observe Automatic Refresh:** As soon as you save the changes, your web browser (which was opened by `npm run dev -- --open`) should automatically refresh, and you will now see the text "Hello World" displayed.

## Congratulations!

You have successfully created and run your first SvelteKit application!
