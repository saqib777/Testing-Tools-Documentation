# Hoppscotch — Web-Based API Testing (Beginner Friendly)

## What is Hoppscotch?

**Hoppscotch** (formerly known as Postwoman) is a free, open-source, web-based API testing tool.  
It lets you send and inspect HTTP requests right from your browser — no installation required.  

You can think of it as a lightweight, online version of Postman or Insomnia, perfect for quick API checks, learning, and collaboration.

Official website: [https://hoppscotch.io](https://hoppscotch.io)

---

## Why use Hoppscotch?
- 🌐 **No installation** — runs entirely in your browser.  
- ⚡ **Fast and minimal** — ideal for quick request testing.  
- 🧩 **Supports REST, GraphQL, WebSocket, and gRPC.**  
- 🧠 **Beginner-friendly** — intuitive UI with live previews and easy variable management.  
- 💾 **Save and sync requests** if you sign in with GitHub or Google.  
- 🧑‍🤝‍🧑 **Collaboration** — share requests via short links or export collections.  
- 🔒 **Privacy** — requests are sent directly from your browser, no server logs by default.

---

## Getting Started (Step-by-Step)

### Step 1: Open Hoppscotch
Go to [https://hoppscotch.io](https://hoppscotch.io).  
No download, no setup — it opens directly in your browser.

### Step 2: Create and Send a Request
1. In the **Request** tab:
   - Select the method: `GET`, `POST`, `PUT`, `DELETE`, etc.  
   - Enter a URL, e.g. `https://jsonplaceholder.typicode.com/posts/1`.  
   - Click **Send**.
2. See the response instantly below — body, headers, and status code.

✅ **Example**:  
Send a `GET` request to:
```
https://jsonplaceholder.typicode.com/users
```
You’ll get a JSON array of user objects.

---

## Step 3: Adding Headers, Params, and Body
- Click **Headers** to add key-value pairs like `Authorization`, `Content-Type`, etc.  
- Click **Params** to add query parameters.  
- For `POST` or `PUT` requests, switch to the **Body** tab and choose format:
  - JSON  
  - Form data  
  - Raw text  
  - GraphQL query  

**Example POST:**
```
POST https://jsonplaceholder.typicode.com/posts
Body (JSON):
{
  "title": "Hello Hoppscotch",
  "body": "Testing made easy",
  "userId": 1
}
```

---

## Step 4: Environments and Variables
Hoppscotch supports environments (like Postman) so you can reuse values across requests.

1. Click **Environments → Create Environment**.  
2. Add variables such as:
   ```json
   {
     "base_url": "https://jsonplaceholder.typicode.com",
     "token": "abcd1234"
   }
   ```
3. In your requests, use `{{ base_url }}/users` or `{{ token }}`.  
When you switch environments, Hoppscotch automatically replaces them.

---

## Step 5: GraphQL, WebSocket & gRPC Testing

### GraphQL:
- Select **GraphQL** tab.  
- Paste your endpoint and query:
  ```graphql
  query {
    users {
      id
      name
    }
  }
  ```
- Click **Send** to see structured results.

### WebSocket:
- Go to **WebSocket** tab.  
- Connect to a server, e.g. `wss://echo.websoc
