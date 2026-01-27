

## 1. What HTTP Actually Is

**HTTP (HyperText Transfer Protocol)** is:

* A **stateless**, **request–response** protocol
* Used between **client (browser / mobile / frontend)** and **server (backend)**

Every interaction is:

```
Client → Request → Server
Server → Response → Client
```

---

## 2. HTTP Request Structure

A request has **3 main parts**:

```
<METHOD> <PATH> <HTTP_VERSION>
Headers
(blank line)
Body (optional)
```

### Example

```
POST /api/users HTTP/1.1
Host: example.com
Content-Type: application/json
Authorization: Bearer xyz123

{
  "name": "Alice",
  "email": "alice@test.com"
}
```

---

## 3. HTTP Methods (VERY important)

Know these cold:

| Method  | Purpose                   |
| ------- | ------------------------- |
| GET     | Read data                 |
| POST    | Create data               |
| PUT     | Replace data              |
| PATCH   | Update part of data       |
| DELETE  | Remove data               |
| HEAD    | Same as GET, no body      |
| OPTIONS | Ask server what’s allowed |

### Backend rule of thumb

* **GET** → no side effects
* **POST** → creates something
* **PUT/PATCH** → updates
* **DELETE** → deletes

---

## 4. HTTP Response Structure

```
HTTP/1.1 <STATUS_CODE> <STATUS_TEXT>
Headers
(blank line)
Body (optional)
```

### Example

```
HTTP/1.1 201 Created
Content-Type: application/json

{
  "id": 42,
  "name": "Alice"
}
```

---

## 5. HTTP Status Codes (MEMORIZE THESE)

Grouped by category:

### 2xx — Success

| Code | Meaning    |
| ---- | ---------- |
| 200  | OK         |
| 201  | Created    |
| 204  | No Content |

### 3xx — Redirects

| Code | Meaning            |
| ---- | ------------------ |
| 301  | Permanent redirect |
| 302  | Temporary redirect |

### 4xx — Client errors

| Code | Meaning                      |
| ---- | ---------------------------- |
| 400  | Bad request                  |
| 401  | Unauthorized (not logged in) |
| 403  | Forbidden (no permission)    |
| 404  | Not found                    |
| 409  | Conflict                     |
| 422  | Validation error             |

### 5xx — Server errors

| Code | Meaning               |
| ---- | --------------------- |
| 500  | Internal server error |
| 502  | Bad gateway           |
| 503  | Service unavailable   |

 **Backend devs choose the status code** — it’s part of your API design.

---

## 6. Headers (Critical for Backend)

Headers are **metadata** about the request or response.

### Common Request Headers

| Header        | Purpose                  |
| ------------- | ------------------------ |
| Host          | Domain                   |
| Authorization | Auth token               |
| Content-Type  | Body format              |
| Accept        | Expected response format |
| User-Agent    | Client info              |
| Cookie        | Session data             |

### Common Response Headers

| Header                      | Purpose         |
| --------------------------- | --------------- |
| Content-Type                | Response format |
| Content-Length              | Body size       |
| Set-Cookie                  | Store cookie    |
| Cache-Control               | Caching rules   |
| Access-Control-Allow-Origin | CORS            |

---

## 7. Content-Type (Super Important)

Tells server **how to parse the body**.

Common types:

```
application/json
application/x-www-form-urlencoded
multipart/form-data
text/plain
```

Backend mistake #1: **Not matching Content-Type with body parsing**

---

## 8. Query Params vs Path Params vs Body

You MUST know the difference:

### Path params

```
GET /users/42
```

→ Identifies a resource

### Query params

```
GET /users?active=true&page=2
```

→ Filters / options

### Body

```
POST /users
{
  "name": "Alice"
}
```

→ Actual data

---

## 9. Statelessness & Sessions

HTTP is **stateless**:

* Server doesn’t remember users by default

Solutions:

* **Cookies + Sessions**
* **JWT tokens**
* **OAuth tokens**

---

## 10. Cookies vs Authorization Header

### Cookies

* Automatically sent by browser
* Used for sessions

### Authorization Header

```
Authorization: Bearer <token>
```

* Explicit
* Preferred for APIs

---

## 11. CORS (Backend Pain Point)

Controls **who can call your API from browsers**.

Important headers:

```
Access-Control-Allow-Origin
Access-Control-Allow-Methods
Access-Control-Allow-Headers
```

Browsers enforce CORS — servers don’t.

---

## 12. HTTP vs HTTPS

* HTTPS = HTTP + TLS encryption
* Protects:

  * Credentials
  * Tokens
  * Data

Backend must:

* Redirect HTTP → HTTPS
* Set secure cookies

---

## 13. Idempotency (Backend Concept)

Same request → same result

| Method | Idempotent |
| ------ | ---------- |
| GET    | ✅          |
| PUT    | ✅          |
| DELETE | ✅          |
| POST   | ❌          |

Important for retries and APIs.

---

## 14. API Design Best Practices

* Use **nouns**, not verbs

  ```
  ❌ /getUsers
  ✅ /users
  ```
* Return proper status codes
* Validate input
* Never trust client data

---

## 15. Tools You Should Know

* **curl**
* **Postman / Insomnia**
* Browser DevTools → Network tab

---


### What an HTTP session is

HTTP itself is **stateless** — every request is independent.
An **HTTP session** is a way for a server to remember a user **across multiple requests** (login state, cart items, preferences, etc.).

### How it works (typical flow)

1. User sends a request (e.g., logs in)
2. Server creates a **session object** (stored in memory, DB, Redis, etc.)
3. Server sends back a **session ID**
4. Browser stores that ID (usually in a **cookie**)
5. On every next request, the browser sends the session ID
6. Server looks up the session data using that ID

### Where session data lives

* **Server-side**:

  * Memory (fast, but not scalable)
  * Database
  * Redis / Memcached (very common)
* **Client-side** (less common):

  * Encrypted cookies (e.g., JWT-style sessions)

### Session vs Cookie

| Feature  | Session              | Cookie                |
| -------- | -------------------- | --------------------- |
| Stored   | Server               | Browser               |
| Size     | Large                | Small (≈4KB)          |
| Security | More secure          | Less secure           |
| Lifetime | Controlled by server | Controlled by browser |

Cookies often **store only the session ID**, not the data.

### Common uses

* User authentication (logged in / logged out)
* Shopping carts
* CSRF protection
* User preferences

### Example (conceptual)

```text
Client → POST /login
Server → Set-Cookie: SESSION_ID=abc123

Client → GET /dashboard (with SESSION_ID)
Server → Loads session abc123 → user = "Alice"
```

### Common pitfalls

* Sessions stored only in memory → break when server restarts
* No expiration → security risk
* Not using HTTPS → session hijacking
* Multiple servers without shared session store → users “randomly logged out”

---

## What is `HttpSession` in Java

In Java web apps (Servlets, JSP, Spring MVC), an **`HttpSession`** lets the server remember a user between HTTP requests.

Package:

```java
import jakarta.servlet.http.HttpSession;
// (or javax.servlet.http.HttpSession in older versions)
```

---

## How it works

1. User sends a request
2. Server creates a session (`HttpSession`)
3. Server sends a **session ID** (`JSESSIONID`) in a cookie
4. Browser sends `JSESSIONID` with every request
5. Server uses it to find the session data

---

## Creating / getting a session

```java
HttpSession session = request.getSession(); // creates if not exists
```

If you *don’t* want to create one automatically:

```java
HttpSession session = request.getSession(false); // returns null if none
```

---

## Storing data in a session

```java
session.setAttribute("username", "Alice");
session.setAttribute("role", "ADMIN");
```

Retrieve it later:

```java
String username = (String) session.getAttribute("username");
```

Remove an attribute:

```java
session.removeAttribute("username");
```

---

## Invalidating a session (logout)

```java
session.invalidate();
```

This:

* clears all attributes
* destroys the session
* makes the `JSESSIONID` useless

---

## Session timeout

Set manually:

```java
session.setMaxInactiveInterval(30 * 60); // 30 minutes (seconds)
```

Or in `web.xml`:

```xml
<session-config>
    <session-timeout>30</session-timeout> <!-- minutes -->
</session-config>
```

---

## Example: Login + protected page

### Login Servlet

```java
protected void doPost(HttpServletRequest request, HttpServletResponse response)
        throws IOException {

    String user = request.getParameter("username");
    String pass = request.getParameter("password");

    if ("admin".equals(user) && "1234".equals(pass)) {
        HttpSession session = request.getSession();
        session.setAttribute("user", user);
        response.sendRedirect("dashboard");
    } else {
        response.sendRedirect("login.jsp?error=true");
    }
}
```

### Protected Servlet

```java
protected void doGet(HttpServletRequest request, HttpServletResponse response)
        throws IOException {

    HttpSession session = request.getSession(false);

    if (session == null || session.getAttribute("user") == null) {
        response.sendRedirect("login.jsp");
        return;
    }

    response.getWriter().println("Welcome!");
}
```

---

## `JSESSIONID`

* Stored in a **cookie**
* Automatically managed by the container (Tomcat, Jetty, etc.)
* Can also be URL-rewritten (not recommended):

```java
response.encodeURL("dashboard");
```

---

## Best practices 

* Always use **HTTPS**
* Call `getSession(false)` for protected pages
* Regenerate session after login (prevent session fixation)
* Don’t store large objects in session
* Avoid storing DB connections in session

---

## Spring Boot note (if relevant)

In Spring:

```java
@GetMapping("/profile")
public String profile(HttpSession session) {
    String user = (String) session.getAttribute("user");
    return "profile";
}
```

---






