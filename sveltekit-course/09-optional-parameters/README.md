# SvelteKit Routing: Optional Parameters

In previous videos, we learned about dynamic route parameters, which are mandatory segments in the URL. This video explores how to make these parameters **optional**, providing default behavior when the parameter is not present in the URL.

## Scenario 7: Optional Language Parameter

Consider a landing page that needs to support multiple languages (English, Spanish, French), with English being the default. We want the following URL behavior:

- `/`: Display content in English ("Hello").
- `/es`: Display content in Spanish ("Hola").
- `/fr`: Display content in French ("Bonjour").

Currently, our root `+page.svelte` displays "Welcome home". We want to modify our routing to handle the optional language parameter.

### Implementation

1.  **Create a Dynamic `lang` Folder:** Inside the `src/routes` folder, create a new folder named `[lang]`. The square brackets indicate a dynamic parameter for the language.

    ```
    src/
    └── routes/
        └── [lang]/
            └── +page.svelte
    ```

2.  **Implement Language-Based Greeting:** In `src/routes/[lang]/+page.svelte`, add a `<script>` block to handle the language logic:

    ```svelte
    <script>
      import { page } from '$app/stores';
      const greetings = {
        en: 'Hello',
        es: 'Hola',
        fr: 'Bonjour'
      };
      const { lang } = $page.params;
      const greeting = greetings[lang] || greetings.en; // Default to English
    </script>

    <h1>{greeting}</h1>
    ```

    Navigating to `/en`, `/es`, or `/fr` will now display the corresponding greeting. However, navigating to `/` still shows the content of the root `+page.svelte` ("Welcome home"), and we want English to be the default.

3.  **Making the Parameter Optional:** To make the `lang` parameter optional, wrap the dynamic folder name with an **additional pair of square brackets**: `[[lang]]`.

    ```
    src/
    └── routes/
        └── [[lang]]/
            └── +page.svelte
    ```

4.  **Resolving Route Conflict:** After making `lang` optional, you might encounter an error in the terminal indicating a route conflict between `/` and `/[[lang]]`. This is because both the `+page.svelte` inside `[[lang]]` and the `+page.svelte` at the root level now potentially match the `/` path.

5.  **Organizing Optional Routes (Marketing Landing Page):** To resolve this and logically group our optional language route, let's create a new folder named `marketing` within `routes` and move the `[[lang]]` folder inside it.

    ```
    src/
    └── routes/
        └── marketing/
            └── [[lang]]/
                └── +page.svelte
    ```

    Now, the URLs will be `/marketing`, `/marketing/es`, `/marketing/fr`, etc.

6.  **Handling the Missing Parameter:** In `src/routes/marketing/[[lang]]/+page.svelte`, we need to provide a default value for the `lang` parameter when it's not present in the URL. We can do this during destructuring:

    ```svelte
    <script>
      import { page } from '$app/stores';
      const greetings = {
        en: 'Hello',
        es: 'Hola',
        fr: 'Bonjour'
      };
      const { lang = 'en' } = $page.params; // Default to 'en' if lang is undefined
      const greeting = greetings[lang];
    </script>

    <h1>{greeting}</h1>
    ```

Now:

- Navigating to `/marketing` will display "Hello" (English default).
- Navigating to `/marketing/es` will display "Hola" (Spanish).
- Navigating to `/marketing/fr` will display "Bonjour" (French).

The language parameter is now optional, with English as the default when no language is specified in the URL.

## Key Takeaway: Optional Dynamic Parameters

- To make a dynamic route parameter optional, wrap its folder name with **double square brackets**: `[[parameterName]]`.
- When a parameter is optional, you need to handle the case where the parameter is not present in the URL, often by providing a default value in your component logic.
- Be mindful of potential route conflicts when making parameters optional, especially with the root route (`/`). Organizing optional routes within subfolders can help manage this.

In the next video, we will learn how to navigate between different routes within our SvelteKit application from the user interface.
