Great! You're really building up a solid foundation with SvelteKit API routes. Let's break down **how to handle POST requests** cleanly and clearly — think of this as your personal guide you can refer back to anytime:

---

# 📨 Handling POST Requests in SvelteKit API Routes

POST requests are used to **create new data**. In this case, you’re adding a new comment to an in-memory array using an API route.

---

## 🧱 Folder & File Structure

We're working in the same API route as before:

```
src/
└── routes/
    └── api/
        └── comments/
            └── +server.js
```

---

## 💬 The Comments Array

Still using mock data from:

```js
// src/lib/comments.js
export const comments = [
  { id: 1, text: "Great video, thanks!" },
  { id: 2, text: "Could you cover form validation next?" },
  { id: 3, text: "Subscribed for more!" },
];
```

---

## 📥 Handling the POST Request

Add this to `+server.js`:

```js
import { comments } from "$lib/comments.js";
import { json } from "@sveltejs/kit";

export async function POST({ request }) {
  const { text } = await request.json();

  const newComment = {
    id: comments.length + 1,
    text,
  };

  comments.push(newComment);

  return json(newComment, { status: 201 }); // 201 Created
}
```

### 🔍 Key Points:

- `POST()` matches the HTTP verb
- `request.json()` parses the body sent by the client
- We create a new object and `push` it to the array
- Response is sent using `json()` with status `201 Created`

---

## 🧪 Testing with Thunder Client

### Request Setup:

- **Method**: POST
- **URL**: `http://[::1]:5173/api/comments`
- **Body (JSON)**:

```json
{
  "text": "This is a new comment!"
}
```

### Response:

```json
{
  "id": 4,
  "text": "This is a new comment!"
}
```

✅ Status: `201 Created`

If you now send a **GET request**, you’ll see your new comment appended to the existing array.

---

## 📌 Summary

- `POST()` lets you **receive data** from the client
- `request.json()` helps parse that incoming data
- Use `json(data, { status })` to return a proper response
- Thunder Client is a great tool to quickly test these routes
- Data is in-memory, so changes disappear on refresh/restart (totally fine for learning)

---

Ready to dive into **Dynamic API Routes** next?

Let me know if you want that one summarized in the same way!
