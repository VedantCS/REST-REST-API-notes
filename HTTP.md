

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

👉 **Backend devs choose the status code** — it’s part of your API design.

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




