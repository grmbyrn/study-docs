---
## 🗑️ DELETE Requests in SvelteKit

A `DELETE` request is used to **remove a specific resource** — in this case, a comment by its ID.
---

## 📁 File Location Recap

Your dynamic API route for handling delete operations lives here:

```
src/
└── routes/
    └── api/
        └── comments/
            └── [commentId]/
                └── +server.js
```

---

## 🧠 The Code: Handling DELETE

```js
import { comments } from "$lib/comments.js";
import { json } from "@sveltejs/kit";

export async function DELETE({ params }) {
  const { commentId } = params;

  const deletedComment = comments.find((c) => c.id === parseInt(commentId));
  const index = comments.findIndex((c) => c.id === parseInt(commentId));

  if (index === -1) {
    return json({ message: "Comment not found" }, { status: 404 });
  }

  comments.splice(index, 1);

  return json(deletedComment);
}
```

---

## 🧪 Testing DELETE in Thunder Client

1. **Method:** `DELETE`
2. **URL:**  
   `http://[::1]:5173/api/comments/4`
3. **No body needed.** You’re only deleting by ID.
4. ✅ **Send**: You should get `200 OK` and the deleted comment returned in the response.

---

## ✅ Confirm with GET

Make a GET request to `/api/comments` to verify that the comment is actually gone.

---

## 💡 Optional: Add Robust Error Handling

Already handled nicely:

```js
if (index === -1) {
  return json({ message: "Comment not found" }, { status: 404 });
}
```

Good stuff — your API is safe from deleting ghosts. 👻

---

## 🧾 Final Section Recap

In this **Routing Module**, you’ve learned:

| Feature             | What You Learned                                           |
| ------------------- | ---------------------------------------------------------- |
| **Pages**           | How file-based routing maps to pages                       |
| **Layouts**         | Nested layouts, layout groups, and breaking out            |
| **Dynamic Routing** | Dynamic `[slug]`, optional `[[id]]`, catch-all `[...rest]` |
| **Navigation**      | Anchor links and programmatic navigation                   |
| **API Routes**      | Defined `+server.js` for GET, POST, PATCH, DELETE          |
| **Best Practices**  | Component and utility colocation in `routes` or `lib`      |

---

## 🔚 End of Routing Section

You’ve got all the tools now to:

- Build complex frontend routes
- Serve custom data from the backend
- Handle RESTful API interactions — all within **SvelteKit**!
