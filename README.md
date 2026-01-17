# REST-REST-API-notes
REST stands for  REpresentational State Transfer. REST is not a protocol or a standard, it is an architectural style. During the development phase, API developers can implement REST in a variety of ways.
A Web API (or Web Service) conforming to the REST architectural style is called a REST API (or RESTful API).

But first... what is an API(Application Programming Interface)?

An API is a way for two programs to talk to each other. Programs use APIs to request and exchange data.

An API:

Exposes functions or endpoints

Accepts requests

Returns responses

for example:
Client → API → Server → API → Client

Most modern apps use REST APIs over HTTP.

## Key terms:
API – the contract

REST – a style of API which follows rest design principles

Endpoint – a URL

Request – what client sends

Response – what server returns

JSON – common data format

## REST vs SOAP (big picture)

Both REST and SOAP are ways to build APIs.
SOAP (older, strict, heavy)

SOAP = Simple Object Access Protocol

Key ideas:

Very strict rules

Uses XML only

Has a fixed message format

Often used in enterprise / legacy systems

REST (modern, simple, popular)
helps to develop all kinds of web applications having all possible CRUD (create, retrieve, update, delete) operations.
REST guidelines suggest using a specific HTTP method on a particular type of call made to the server
Key ideas

Uses normal HTTP

Uses URLs + HTTP methods

Usually returns JSON

Simple & lightweight


HTTP methods (very important for REST)
REST APIs use HTTP methods/verbs to describe actions:

| Method | Meaning     | Example     |
| ------ | ----------- | ----------- |
| GET    | Read data   | Get user    |
| POST   | Create data | Create user |
| PUT    | Update data | Update user |
| DELETE | Remove data | Delete user |


| Method | Action | Changes Data? |
| ------ | ------ | ------------- |
| GET    | Read   | ❌             |
| POST   | Create | ✅             |
| PUT    | Update | ✅             |
| DELETE | Delete | ✅             |

REST APIs are built around:

URLs = what resource

HTTP methods = what action

## HTTP STATUS CODE:
| Range | Meaning      |
| ----- | ------------ |
| 2xx   | Success      |
| 4xx   | Client error |
| 5xx   | Server error |

| Scenario                 | Status | 
| ------------------------ | ------ |
| Successfully fetch data  | 200    |
| Successfully create data | 201    |
| Resource not found       | 404    |
| Invalid input            | 400    |
| Backend crash            | 500    |

| HTTP Method | Possible Status Codes | Used when                                                                                |
| ----------- | --------------------- | ---------------------------------------------------------------------------------------- |
| **GET**     | 200, 404              | 200 → data fetched successfully<br>404 → resource not found                              |
| **POST**    | 201, 400              | 201 → resource created<br>400 → invalid request body                                     |
| **PUT**     | 200, 400, 404         | 200 → resource updated<br>400 → invalid update data<br>404 → resource not found          |
| **DELETE**  | 200, 204, 404         | 200 → deleted with response<br>204 → deleted with no content<br>404 → resource not found |
| **ERROR**   | 500                   | Server-side failure (exception, crash)                                                   |

