# Insomnia — API Testing (Beginner Friendly)

## What is Insomnia?
**Insomnia** is an open-source API client that lets you send HTTP requests, inspect responses, and organize API collections — similar to Postman, but cleaner and lighter.  
It’s great for **beginners**, developers, and testers who want a fast, distraction-free tool for exploring and testing APIs without heavy setup.

Official site: [https://insomnia.rest](https://insomnia.rest)

---

## Why use Insomnia?
-  **Simple interface** – minimalist design with fewer menus and distractions.  
-  **Supports REST, GraphQL, gRPC, and WebSocket testing.**  
-  **Environment variables & workspaces** – easy to manage multiple environments.  
-  **Authentication helpers** – supports Basic, Bearer, OAuth 2.0, API Key, etc.  
-  **Cross-platform** – works on Windows, macOS, and Linux.  
-  **Import/export compatibility** – you can import Postman collections or OpenAPI specs.

---

## Getting Started (Step by Step)

### Step 1: Install
Download Insomnia from the official site: [https://insomnia.rest/download](https://insomnia.rest/download)  
Install it on your OS like a normal desktop app.

### Step 2: Create a Workspace
- Click **Create → Workspace → New Design Document** (for API spec) or **New Request Collection** (for testing).  
- Name it e.g., “Sample API Tests”.

### Step 3: Create Your First Request
1. Click **New Request → GET**.  
2. Enter the URL: `https://jsonplaceholder.typicode.com/posts/1`  
3. Hit **Send**.  
4. You’ll see the response with headers, status, and body.  
   **Tip:** Try changing method to POST or PUT to experiment.

### Step 4: Add Environment Variables
- Click the **Manage Environments** icon (top-right gear).  
- Define variables like:
  ```json
  {
    "base_url": "https://jsonplaceholder.typicode.com",
    "user_id": 1
  }
  ```
- Use variables in requests like:  
  `{{ base_url }}/users/{{ user_id }}`

### Step 5: Write Basic Tests (via Insomnia Response Validation)
Insomnia supports simple test scripts using the built-in **Tests tab** with JavaScript syntax.
```js
const response = insomnia.response.json();
expect(response.id).to.equal(1);
expect(insomnia.response.status).to.equal(200);
```
 These are powered by the Chai assertion library and run after the request.

---

## Useful Features for Beginners

| Feature | What it does | Why it’s helpful |
|----------|---------------|-----------------|
| **History** | Keeps a record of sent requests | Quickly retry or compare results |
| **Collections** | Group related API calls | Keeps your workspace organized |
| **Environments** | Variables for URLs, tokens, etc. | Run the same tests across multiple systems |
| **Code Generator** | Converts a request into code snippets (Python, JS, cURL) | Great for learning API integration |
| **Plugins** | Extend Insomnia (JWT decoder, AWS signer, etc.) | Add capabilities without code |

---

## Example: Simple CRUD Flow
Here’s a practical mini example using a public API:

1. **GET** all users  
   URL: `{{ base_url }}/users`  
   Expect status 200.

2. **POST** a new user  
   URL: `{{ base_url }}/users`  
   Body (JSON):
   ```json
   {
     "name": "Jane Doe",
     "email": "jane@example.com"
   }
   ```
   Expect status 201.

3. **GET** created user (with returned ID).  
   URL: `{{ base_url }}/users/{{ new_user_id }}`  

4. **DELETE** user  
   URL: `{{ base_url }}/users/{{ new_user_id }}`  

You can script the “Tests” tab for each request to assert status codes and save response data into environment variables.

---

## Best Practices
-  Use **environments** for different setups (Dev, QA, Prod).  
-  Use the **Tests tab** for lightweight validation (status, keys, schema).  
-  Group requests logically in **folders or collections**.  
-  Store secrets safely — avoid committing tokens to Git.  
-  Export your workspace or sync to the cloud for backup.  
-  Combine with Git integration (Insomnia Sync supports version control).

---

## Pros and Cons

**Pros**
- Lightweight, fast, and free.  
- Supports REST, GraphQL, and gRPC out of the box.  
- Beginner-friendly for manual API exploration.  
- Simple environment and variable handling.  
- Integrates with Git for versioning (Insomnia Cloud).

**Cons**
- Limited automation features (no collection runner like Postman).  
- No built-in load testing or CI runner — geared toward manual use.  
- Scriptable tests are basic compared to full frameworks.  

---

## Example: Save Response to Variable
You can use `setEnvironmentVariable` in the Test tab:
```js
const json = insomnia.response.json();
setEnvironmentVariable("userId", json.id);
```
Now `{{ userId }}` is available for the next requests.

---

## Common Use Cases
- Quick manual validation of APIs during development.  
- Testing endpoints before writing automation.  
- Debugging failed CI/CD requests (by replicating payloads easily).  
- Learning HTTP basics — status codes, headers, methods.  

---

## Resources & Learning Links
- Official docs → [https://docs.insomnia.rest](https://docs.insomnia.rest)  
- Plugin hub → [https://insomnia.rest/plugins](https://insomnia.rest/plugins)  
- Tutorials:  
  - [How to use Insomnia for API Testing (FreeCodeCamp Guide)](https://www.freecodecamp.org/news/how-to-test-apis-using-insomnia/)  
  - [Insomnia Docs: Environment Variables](https://docs.insomnia.rest/insomnia/environment-variables)  
- GitHub (open source): [https://github.com/Kong/insomnia](https://github.com/Kong/insomnia)

---

## When to Use Insomnia
**Use it when**
- You’re learning or testing small APIs manually.  
- You prefer simplicity over features.  
- You’re debugging API calls locally.  

**Not ideal when**
- You need automated regression or CI testing — use Postman + Newman, RestAssured, or similar.  
- You need full load or security scanning.  

---

## Summary
**Insomnia** is a clean, fast, beginner-friendly API client that helps you understand and test REST/GraphQL APIs with minimal setup.  
It’s perfect for developers and QA engineers learning API testing, exploring endpoints, or debugging services — a great next step after Postman for those who prefer simplicity and focus.

