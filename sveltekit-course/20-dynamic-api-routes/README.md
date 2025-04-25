Awesome — you're cruising through the SvelteKit API journey! Let’s zoom in on **Dynamic API Routes** and break this video down into digestible steps so you can come back to it any time.

---

## 🔄 Dynamic API Routes in SvelteKit

This is how we handle routes like:

```
/api/comments/1
/api/comments/2
```

Where the number (`1`, `2`, etc.) is a **dynamic segment** — like a placeholder for the `commentId`.

---

## 🧱 Folder & File Structure

Here's how to create the route:

```
src/
└── routes/
    └── api/
        └── comments/
            └── [commentId]/
                └── +server.js
```

> `commentId` inside square brackets means it's a dynamic parameter.

---

## 🧠 The Code: Handling a GET Request for a Single Comment

Inside `+server.js`:

```js
import { comments } from "$lib/comments.js";
import { json } from "@sveltejs/kit";

export function GET({ params }) {
  const { commentId } = params;
  const comment = comments.find((c) => c.id === parseInt(commentId));

  return json(comment);
}
```

### 🔍 What’s Happening Here:

- `params.commentId` gives us the dynamic segment from the URL
- `parseInt(commentId)` ensures we match against numeric IDs
- We find the matching comment and return it as JSON

---

## 🧪 Testing It in Thunder Client

Use **GET** requests to these URLs:

- `http://[::1]:5173/api/comments/1` → returns the first comment
- `http://[::1]:5173/api/comments/2` → returns the second comment
- `http://[::1]:5173/api/comments/4` → returns the new comment we added in the POST example

✅ You should see each comment returned individually based on ID.

---

## 💡 Tip

If a comment with that ID doesn’t exist, you may want to return a `404` like this:

```js
if (!comment) {
  return json({ message: "Comment not found" }, { status: 404 });
}
```

---

## 📌 Summary

- Dynamic segments in API routes = folder with `[param]`
- Use `params` from the request event to access the dynamic value
- Great for fetching, updating, or deleting individual records

---

You’re now all set to **PATCH** or **DELETE** individual comments — we’ll jump into that next.

Want me to break that one down in the same easy-to-skim format too?
