# Network Programming Using Python with FastAPI - Complete Guide
## Application Layer Network Programming

---

## Table of Contents

1. [Introduction](#introduction)
2. [Fundamentals of Network Programming](#fundamentals-of-network-programming)
3. [OSI Model and Application Layer](#osi-model-and-application-layer)
4. [Introduction to FastAPI](#introduction-to-fastapi)
5. [Setting Up FastAPI Development Environment](#setting-up-fastapi-development-environment)
6. [FastAPI Basics and Core Concepts](#fastapi-basics-and-core-concepts)
7. [HTTP Protocol and Methods](#http-protocol-and-methods)
8. [Request and Response Handling](#request-and-response-handling)
9. [Path Parameters and Query Parameters](#path-parameters-and-query-parameters)
10. [Request Body and Data Validation](#request-body-and-data-validation)
11. [Response Models and Status Codes](#response-models-and-status-codes)
12. [Error Handling and Exception Management](#error-handling-and-exception-management)
13. [Middleware in FastAPI](#middleware-in-fastapi)
14. [CORS and Security Headers](#cors-and-security-headers)
15. [Authentication and Authorization](#authentication-and-authorization)
16. [JWT Token Implementation](#jwt-token-implementation)
17. [OAuth2 Integration](#oauth2-integration)
18. [File Upload and Download Management](#file-upload-and-download-management)
19. [WebSocket Communication](#websocket-communication)
20. [RESTful API Design Principles](#restful-api-design-principles)
21. [Database Integration with FastAPI](#database-integration-with-fastapi)
22. [SQLAlchemy ORM Integration](#sqlalchemy-orm-integration)
23. [Async and Await in FastAPI](#async-and-await-in-fastapi)
24. [Dependency Injection System](#dependency-injection-system)
25. [Testing FastAPI Applications](#testing-fastapi-applications)
26. [Example Projects](#example-projects)
27. [Best Practices and Performance Optimization](#best-practices-and-performance-optimization)
28. [Deployment and Production Considerations](#deployment-and-production-considerations)
29. [Real-World Use Cases](#real-world-use-cases)
30. [Troubleshooting and Common Issues](#troubleshooting-and-common-issues)
31. [Additional Resources and References](#additional-resources-and-references)

---

## 1. Introduction {#introduction}

### What is Network Programming?

Network programming is the practice of developing software applications that communicate over networks, specifically through the Internet or local area networks (LANs). It involves the creation of applications that can send and receive data across network interfaces using standardized protocols.

### What is the Application Layer?

The Application Layer is the topmost layer (Layer 7) in the OSI (Open Systems Interconnection) model, where end-user services and applications interact directly with the network. It is where protocols such as HTTP, HTTPS, FTP, SMTP, DNS, and WebSocket operate. This layer provides network services directly to user applications and is responsible for managing application-level communication.

### Why FastAPI for Network Programming?

FastAPI is a modern, high-performance web framework for building APIs with Python. Key reasons for choosing FastAPI include:

- **Speed**: One of the fastest Python frameworks available
- **Modern Python Features**: Built on top of Python 3.6+ type hints and async support
- **Automatic Documentation**: Generates interactive API documentation automatically
- **Validation**: Built-in request and response validation using Pydantic
- **Async Support**: Native support for asynchronous programming
- **Security**: Built-in authentication and security mechanisms
- **Easy to Learn**: Simple and intuitive API design
- **Production Ready**: Can be deployed to production environments easily

### What You Will Learn

This comprehensive guide covers:
- Fundamental network programming concepts
- FastAPI framework basics and advanced features
- Application-layer protocol implementation
- RESTful API design and development
- Real-time communication with WebSockets
- Security and authentication mechanisms
- Database integration and ORM usage
- Testing and deployment strategies

---

## 2. Fundamentals of Network Programming {#fundamentals-of-network-programming}

### Basic Networking Concepts

#### IP Address (Internet Protocol Address)

An IP address is a unique numerical label assigned to each device connected to a computer network that uses Internet Protocol for communication. There are two versions:

- **IPv4**: 32-bit address format (e.g., 192.168.1.1)
- **IPv6**: 128-bit address format (e.g., 2001:0db8:85a3:0000:0000:8a2e:0370:7334)

#### Port Numbers

A port number is a 16-bit numerical identifier used to identify specific processes or services running on a network device. Port numbers range from 0 to 65535 and are divided into:

- **Well-Known Ports** (0-1023): Reserved for standard services (HTTP: 80, HTTPS: 443, FTP: 21)
- **Registered Ports** (1024-49151): Assigned for specific services
- **Dynamic/Private Ports** (49152-65535): Available for custom applications

#### Network Sockets

A socket is an endpoint for network communication, implementing one end of a network connection. It is defined by the combination of:

- Protocol (TCP, UDP, etc.)
- Local IP Address
- Local Port Number
- Remote IP Address (if connected)
- Remote Port Number (if connected)

#### TCP/IP Protocol Suite

The TCP/IP model consists of four layers:

1. **Link Layer**: Hardware addressing and operation
2. **Internet Layer**: IP addressing and routing
3. **Transport Layer**: TCP, UDP protocols for data delivery
4. **Application Layer**: HTTP, FTP, SMTP, DNS, and other protocols

### Client-Server Architecture

Client-Server is a fundamental architecture in network programming where:

- **Client**: Initiates requests to the server
- **Server**: Listens for and responds to client requests
- Communication typically follows a request-response pattern

### Request-Response Model

The request-response model is the standard communication pattern:

1. Client sends a request to the server
2. Server receives and processes the request
3. Server sends a response back to the client
4. Client receives the response and processes it

---

## 3. OSI Model and Application Layer {#osi-model-and-application-layer}

### OSI Model Overview

The OSI (Open Systems Interconnection) model is a conceptual framework that standardizes the functions of a telecommunication or computing system into seven layers:

| Layer | Name | Examples |
|-------|------|----------|
| 7 | Application Layer | HTTP, HTTPS, FTP, SMTP, DNS, WebSocket |
| 6 | Presentation Layer | Encryption, Compression, Translation |
| 5 | Session Layer | Session management, Dialog control |
| 4 | Transport Layer | TCP, UDP, SCTP |
| 3 | Network Layer | IP (IPv4, IPv6), ICMP, Routing |
| 2 | Data Link Layer | Ethernet, PPP, MAC addressing |
| 1 | Physical Layer | Cables, Signals, Voltage levels |

### Application Layer (Layer 7) in Detail

The Application Layer is where software applications directly provide services to end-users. Key characteristics:

- **User Interaction**: Direct interaction with end-user applications
- **Service Provision**: Provides network services like web browsing, email, file transfer
- **Protocol Usage**: Implements protocols that define how applications communicate
- **Data Format**: Works with data in user-friendly formats (text, images, documents)
- **No Network Details**: Applications don't directly handle network routing or low-level transmission

### Key Application Layer Protocols

#### HTTP/HTTPS (Hypertext Transfer Protocol)

HTTP is the foundation of the World Wide Web and uses a request-response model:

- **Stateless**: Each request is independent
- **Methods**: GET, POST, PUT, DELETE, PATCH, OPTIONS, HEAD, TRACE
- **Port**: 80 (HTTP), 443 (HTTPS)
- **Versions**: HTTP/1.1, HTTP/2, HTTP/3

#### WebSocket

WebSocket provides full-duplex communication channels over a single TCP connection:

- **Persistent Connection**: Long-lived connection between client and server
- **Bidirectional**: Both client and server can initiate messages
- **Real-time**: Low-latency communication
- **Port**: 80 (ws), 443 (wss)

#### DNS (Domain Name System)

DNS translates domain names to IP addresses:

- **Hierarchical System**: Root, TLD, and authoritative nameservers
- **Port**: 53 (UDP and TCP)
- **Query Types**: A, AAAA, CNAME, MX, TXT, SOA

#### SMTP (Simple Mail Transfer Protocol)

SMTP is used for sending emails:

- **Port**: 25 (unencrypted), 465 (SMTPS), 587 (TLS)
- **Authentication**: Required for most modern servers
- **Message Format**: Follows RFC 5321 specifications

#### FTP (File Transfer Protocol)

FTP is used for transferring files between clients and servers:

- **Ports**: 20 (data), 21 (control)
- **Modes**: Active and Passive
- **Authentication**: Username and password

### How FastAPI Fits Into the Application Layer

FastAPI operates entirely at the Application Layer:

- **Protocol**: Implements HTTP/HTTPS and WebSocket protocols
- **Services**: Provides API endpoints for client consumption
- **Data Format**: Works with JSON, XML, and other data formats
- **No Network Layer Involvement**: Delegates to the operating system's TCP/IP stack

---

## 4. Introduction to FastAPI {#introduction-to-fastapi}

### What is FastAPI?

FastAPI is a modern, open-source Python web framework for building APIs (Application Programming Interfaces) with minimal boilerplate code. It is built on top of several foundational libraries:

- **Starlette**: For web framework functionality
- **Pydantic**: For data validation and settings management
- **Uvicorn**: An ASGI (Asynchronous Server Gateway Interface) web server

### Key Features of FastAPI

#### Type Hints and Python 3.6+ Features

FastAPI leverages Python's type hint system for:

- Automatic request validation
- Automatic response serialization
- IDE code completion and type checking
- Self-documenting code

#### High Performance

FastAPI is one of the fastest Python frameworks because:

- Async/await native support
- Efficient request routing
- Minimal overhead
- Benchmarked to be nearly as fast as Node.js and Go

#### Automatic API Documentation

FastAPI automatically generates interactive documentation:

- **Swagger UI**: Interactive API explorer available at `/docs`
- **ReDoc**: Alternative documentation available at `/redoc`
- **OpenAPI**: Machine-readable schema at `/openapi.json`

#### Built-in Validation

Pydantic provides automatic request/response validation using type hints:

- Type conversion
- Default values
- Range validation
- Custom validators
- Error messages

#### Security Features

FastAPI includes built-in security mechanisms:

- OAuth2 implementation
- JWT token support
- API key authentication
- CORS handling
- HTTPS support

#### Async and Concurrency

Native support for async programming:

- Async functions (coroutines)
- Non-blocking I/O operations
- Efficient handling of many concurrent connections
- Integration with async libraries

### FastAPI vs Other Python Frameworks

| Framework | Speed | Documentation | Learning Curve | Async Support |
|-----------|-------|---------------|-----------------|---------------|
| FastAPI | Very Fast | Excellent | Moderate | Native |
| Django | Moderate | Excellent | Steep | Limited |
| Flask | Slow | Good | Easy | Limited |
| Tornado | Fast | Good | Moderate | Native |
| Sanic | Very Fast | Fair | Moderate | Native |

---

## 5. Setting Up FastAPI Development Environment {#setting-up-fastapi-development-environment}

### Prerequisites

Before setting up FastAPI, ensure you have:

- **Python**: Version 3.7 or higher installed
- **pip**: Python package manager
- **Virtual Environment**: Recommended for isolation
- **Code Editor**: VS Code, PyCharm, or similar

### Step-by-Step Installation Guide

#### Step 1: Create a Project Directory

```bash
mkdir fastapi_project
cd fastapi_project
```

#### Step 2: Create a Virtual Environment

On Windows:
```bash
python -m venv venv
venv\Scripts\activate
```

On macOS/Linux:
```bash
python3 -m venv venv
source venv/bin/activate
```

#### Step 3: Install FastAPI and Uvicorn

```bash
pip install fastapi uvicorn[standard]
```

#### Step 4: Verify Installation

```bash
python -c "import fastapi; print(fastapi.__version__)"
```

### Required Dependencies

Core dependencies for FastAPI development:

- **fastapi**: The web framework
- **uvicorn[standard]**: ASGI server with optional dependencies
- **pydantic**: Data validation library
- **starlette**: Web toolkit that FastAPI is built on

### Optional but Recommended Dependencies

For a complete development setup, also install:

```bash
pip install pytest pytest-asyncio httpx python-jose passlib python-dotenv sqlalchemy aiosqlite
```

**Breakdown of optional packages**:

- **pytest**: Unit testing framework
- **pytest-asyncio**: Async test support
- **httpx**: HTTP client for testing
- **python-jose**: JWT token handling
- **passlib**: Password hashing
- **python-dotenv**: Environment variable management
- **sqlalchemy**: ORM for database operations
- **aiosqlite**: Async SQLite driver

### Project Structure

Recommended project structure for FastAPI applications:

```
fastapi_project/
├── main.py                 # Entry point
├── app/
│   ├── __init__.py
│   ├── api/
│   │   ├── __init__.py
│   │   ├── endpoints/
│   │   │   ├── __init__.py
│   │   │   ├── users.py
│   │   │   └── items.py
│   │   └── dependencies.py
│   ├── core/
│   │   ├── __init__.py
│   │   ├── config.py
│   │   └── security.py
│   ├── db/
│   │   ├── __init__.py
│   │   ├── base.py
│   │   └── session.py
│   └── models/
│       ├── __init__.py
│       ├── user.py
│       └── item.py
├── tests/
│   ├── __init__.py
│   ├── test_api.py
│   └── test_users.py
├── requirements.txt
└── .env
```

---

## 6. FastAPI Basics and Code Concepts {#fastapi-basics-and-core-concepts}

### Creating Your First FastAPI Application

#### Minimal Example

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
async def read_root():
    return {"message": "Hello, World!"}
```

Run with:
```bash
uvicorn main:app --reload
```

#### Understanding the Code

- **FastAPI()**: Creates an instance of the FastAPI application
- **@app.get("/")**: Decorator that creates a GET endpoint at the root path
- **async def**: Async function for non-blocking I/O
- **return**: Automatically serialized to JSON

### Application Initialization Options

#### Basic Initialization

```python
from fastapi import FastAPI

app = FastAPI()
```

#### With Metadata

```python
from fastapi import FastAPI

app = FastAPI(
    title="My API",
    description="This is a detailed API description",
    version="1.0.0",
    terms_of_service="https://example.com/terms/",
    contact={
        "name": "API Support",
        "url": "https://example.com/support",
        "email": "support@example.com",
    },
    license_info={
        "name": "Apache 2.0",
        "url": "https://www.apache.org/licenses/LICENSE-2.0.html",
    },
)
```

#### With Documentation URLs

```python
app = FastAPI(
    docs_url="/api/docs",
    redoc_url="/api/redoc",
    openapi_url="/api/openapi.json"
)
```

### Startup and Shutdown Events

```python
from fastapi import FastAPI

app = FastAPI()

@app.on_event("startup")
async def startup_event():
    print("Application starting up")
    # Initialize database connections
    # Load cache
    # Start background tasks

@app.on_event("shutdown")
async def shutdown_event():
    print("Application shutting down")
    # Close database connections
    # Cleanup resources
    # Stop background tasks
```

### Lifespan Context Manager (FastAPI 0.93+)

```python
from contextlib import asynccontextmanager
from fastapi import FastAPI

@asynccontextmanager
async def lifespan(app: FastAPI):
    # Startup
    print("Application starting")
    yield
    # Shutdown
    print("Application shutting down")

app = FastAPI(lifespan=lifespan)
```

### Application Tags

Tags help organize endpoints in documentation:

```python
@app.get("/items/", tags=["items"])
async def read_items():
    return [{"name": "Item 1"}]

@app.get("/users/", tags=["users"])
async def read_users():
    return [{"name": "User 1"}]
```

---

## 7. HTTP Protocol and Methods {#http-protocol-and-methods}

### HTTP Protocol Overview

HTTP (Hypertext Transfer Protocol) is a stateless, application-level protocol used for distributed, collaborative, and hypermedia information systems. Key characteristics:

- **Request-Response**: Client initiates request, server responds
- **Stateless**: Each request is independent
- **Methods**: Different operations identified by HTTP methods
- **Status Codes**: Server response status indicated by numbers
- **Headers**: Metadata sent with requests and responses

### HTTP Methods (Verbs)

HTTP methods define the action to be performed on a resource:

#### GET - Retrieve Data

Requests data from a server without modifying it.

```python
@app.get("/items/{item_id}")
async def read_item(item_id: int):
    return {"item_id": item_id, "name": "Item"}
```

**Characteristics**:
- Idempotent: Multiple calls produce the same result
- Safe: Does not modify data on server
- Cacheable: Response can be cached
- No request body

#### POST - Create Data

Submits data to create a new resource on the server.

```python
@app.post("/items/")
async def create_item(item: dict):
    return {"created": item}
```

**Characteristics**:
- Not idempotent: Multiple calls may create multiple resources
- Not safe: Modifies data on server
- Not cacheable by default
- Uses request body for data transmission

#### PUT - Replace Data

Replaces an entire resource on the server.

```python
@app.put("/items/{item_id}")
async def update_item(item_id: int, item: dict):
    return {"item_id": item_id, "updated": item}
```

**Characteristics**:
- Idempotent: Multiple calls produce the same result
- Not safe: Modifies data on server
- Expects complete resource representation
- Uses request body

#### PATCH - Partial Update

Partially updates a resource.

```python
@app.patch("/items/{item_id}")
async def partial_update_item(item_id: int, item: dict):
    return {"item_id": item_id, "partially_updated": item}
```

**Characteristics**:
- May or may not be idempotent depending on implementation
- Not safe: Modifies data on server
- Allows partial resource updates
- Uses request body

#### DELETE - Remove Data

Deletes a resource from the server.

```python
@app.delete("/items/{item_id}")
async def delete_item(item_id: int):
    return {"deleted": item_id}
```

**Characteristics**:
- Idempotent: Multiple calls produce same result
- Not safe: Modifies data on server
- Should return success status
- Typically no request body

#### HEAD - Metadata Only

Like GET but without the response body.

```python
@app.head("/items/{item_id}")
async def head_item(item_id: int):
    return None
```

**Characteristics**:
- Idempotent
- Safe
- Used for metadata retrieval
- No response body

#### OPTIONS - Describe Options

Describes communication options available.

```python
@app.options("/items/")
async def options_items():
    return {"Allow": "GET, POST, OPTIONS"}
```

**Characteristics**:
- Safe
- Idempotent
- Returns allowed methods in Allow header
- No response body

#### TRACE - Diagnostic Trace

Used for diagnostic purposes (rarely used in modern APIs).

```python
@app.trace("/items/")
async def trace_items():
    return {"trace": "request"}
```

### HTTP Status Codes

Status codes indicate the result of an HTTP request:

#### 1xx - Informational

| Code | Name | Meaning |
|------|------|---------|
| 100 | Continue | Preliminary information |
| 101 | Switching Protocols | Protocol upgrade |

#### 2xx - Success

| Code | Name | Meaning |
|------|------|---------|
| 200 | OK | Request successful |
| 201 | Created | Resource created |
| 202 | Accepted | Request accepted for processing |
| 204 | No Content | Success but no content to return |

#### 3xx - Redirection

| Code | Name | Meaning |
|------|------|---------|
| 301 | Moved Permanently | Permanent redirect |
| 302 | Found | Temporary redirect |
| 304 | Not Modified | Resource not modified |

#### 4xx - Client Error

| Code | Name | Meaning |
|------|------|---------|
| 400 | Bad Request | Invalid request |
| 401 | Unauthorized | Authentication required |
| 403 | Forbidden | Access denied |
| 404 | Not Found | Resource not found |
| 405 | Method Not Allowed | HTTP method not allowed |
| 422 | Unprocessable Entity | Validation error |
| 429 | Too Many Requests | Rate limit exceeded |

#### 5xx - Server Error

| Code | Name | Meaning |
|------|------|---------|
| 500 | Internal Server Error | Server error |
| 501 | Not Implemented | Not implemented |
| 502 | Bad Gateway | Invalid response from upstream |
| 503 | Service Unavailable | Server temporarily unavailable |

### HTTP Headers

Headers provide metadata about the request or response:

#### Common Request Headers

| Header | Purpose |
|--------|---------|
| Content-Type | Media type of request body |
| Accept | Media types client accepts |
| Authorization | Authentication credentials |
| User-Agent | Client application information |
| Accept-Language | Preferred languages |

#### Common Response Headers

| Header | Purpose |
|--------|---------|
| Content-Type | Media type of response body |
| Content-Length | Size of response body |
| Set-Cookie | Cookie to set on client |
| Cache-Control | Caching directives |
| Access-Control-Allow-Origin | CORS origin allowance |

#### Setting Headers in FastAPI

```python
from fastapi import FastAPI
from fastapi.responses import JSONResponse

app = FastAPI()

@app.get("/items/")
async def read_items():
    return JSONResponse(
        content={"items": []},
        headers={"X-Custom-Header": "Custom-Value"}
    )
```

---

## 8. Request and Response Handling {#request-and-response-handling}

### Understanding Requests

A request is data sent from a client to the server, consisting of:

- **Method**: HTTP verb (GET, POST, etc.)
- **URL**: Resource path
- **Headers**: Metadata about the request
- **Body**: Data being sent (optional for POST, PUT, PATCH)
- **Query Parameters**: Key-value pairs in the URL

### Accessing Request Information

```python
from fastapi import FastAPI, Request

app = FastAPI()

@app.get("/info/")
async def get_request_info(request: Request):
    return {
        "method": request.method,
        "url": str(request.url),
        "client": request.client.host if request.client else None,
        "headers": dict(request.headers),
        "query_params": dict(request.query_params),
    }
```

### Request Body

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    name: str
    description: str = None
    price: float

@app.post("/items/")
async def create_item(item: Item):
    return item
```

### Multiple Request Bodies

```python
from fastapi import FastAPI, Body
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    name: str
    price: float

class User(BaseModel):
    username: str
    email: str

@app.post("/items/")
async def create_item_and_user(item: Item, user: User):
    return {"item": item, "user": user}
```

### Embedding Request Body

By default, when a request has a single field, FastAPI expects the field directly. To embed it:

```python
from fastapi import FastAPI, Body
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    name: str
    price: float

@app.post("/items/")
async def create_item(item: Item = Body(..., embed=True)):
    return item
```

### Understanding Responses

A response is data sent from the server back to the client, consisting of:

- **Status Code**: HTTP status code
- **Headers**: Metadata about the response
- **Body**: The actual response data

### Response Models and Serialization

FastAPI automatically serializes response models to JSON:

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    name: str
    price: float

@app.get("/items/", response_model=list[Item])
async def get_items():
    return [
        {"name": "Item 1", "price": 9.99},
        {"name": "Item 2", "price": 19.99}
    ]
```

### Controlling Response Serialization

#### Using Response Model Parameters

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    name: str
    price: float
    tax: float = 0

@app.get("/items/", response_model=list[Item], response_model_exclude_unset=True)
async def get_items():
    return [{"name": "Item 1", "price": 9.99}]
```

Response model parameters:

- **response_model_exclude_unset**: Exclude fields not explicitly set
- **response_model_exclude_defaults**: Exclude fields with default values
- **response_model_exclude**: Exclude specific fields
- **response_model_include**: Include only specific fields

### Custom Response Classes

```python
from fastapi import FastAPI
from fastapi.responses import HTMLResponse, FileResponse, PlainTextResponse

app = FastAPI()

@app.get("/html/", response_class=HTMLResponse)
async def get_html():
    return "<h1>Hello World</h1>"

@app.get("/text/", response_class=PlainTextResponse)
async def get_text():
    return "Plain text response"

@app.get("/file/", response_class=FileResponse)
async def get_file():
    return "path/to/file.pdf"
```

### JSON Response with Custom Parameters

```python
from fastapi import FastAPI
from fastapi.responses import JSONResponse

app = FastAPI()

@app.get("/items/")
async def read_items():
    return JSONResponse(
        content={"items": []},
        status_code=200,
        headers={"X-Custom-Header": "value"},
        media_type="application/json"
    )
```

---

## 9. Path Parameters and Query Parameters {#path-parameters-and-query-parameters}

### Path Parameters

Path parameters are variable parts of the URL path used to identify specific resources.

#### Basic Path Parameter

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/items/{item_id}")
async def read_item(item_id: int):
    return {"item_id": item_id}
```

Accessing `/items/42` returns `{"item_id": 42}`

#### Type Validation

FastAPI automatically validates path parameter types:

```python
@app.get("/items/{item_id}")
async def read_item(item_id: int):
    return {"item_id": item_id}
```

- Accessing `/items/42` returns data
- Accessing `/items/invalid` returns a validation error (422)

#### Multiple Path Parameters

```python
@app.get("/users/{user_id}/items/{item_id}")
async def read_user_item(user_id: int, item_id: int):
    return {"user_id": user_id, "item_id": item_id}
```

#### Path Parameter Constraints

Use Annotated for more detailed constraints:

```python
from fastapi import FastAPI, Path
from typing import Annotated

app = FastAPI()

@app.get("/items/{item_id}")
async def read_item(
    item_id: Annotated[int, Path(..., gt=0)] 
):
    return {"item_id": item_id}
```

Constraint options:

- **gt**: Greater than
- **gte**: Greater than or equal
- **lt**: Less than
- **lte**: Less than or equal
- **min_length**: Minimum string length
- **max_length**: Maximum string length
- **pattern**: Regex pattern for validation

### Query Parameters

Query parameters are key-value pairs appended to the URL after a question mark.

#### Basic Query Parameter

```python
@app.get("/items/")
async def read_items(skip: int = 0, limit: int = 10):
    return {"skip": skip, "limit": limit}
```

Examples:
- `/items/` → `{"skip": 0, "limit": 10}`
- `/items/?skip=20` → `{"skip": 20, "limit": 10}`
- `/items/?skip=20&limit=5` → `{"skip": 20, "limit": 5}`

#### Optional Query Parameters

```python
@app.get("/items/")
async def read_items(q: str = None):
    return {"q": q}
```

- `/items/` → `{"q": None}`
- `/items/?q=search` → `{"q": "search"}`

#### Multiple Query Parameters

```python
@app.get("/items/")
async def read_items(skip: int = 0, limit: int = 10, q: str = None):
    return {"skip": skip, "limit": limit, "q": q}
```

### Query Parameter Validation

```python
from fastapi import FastAPI, Query
from typing import Annotated

app = FastAPI()

@app.get("/items/")
async def read_items(
    q: Annotated[str, Query(..., min_length=3, max_length=50)]
):
    return {"q": q}
```

Validation parameters:

- **min_length**: Minimum string length
- **max_length**: Maximum string length
- **pattern**: Regex pattern
- **examples**: Example values for documentation
- **deprecated**: Mark as deprecated

### List Query Parameters

```python
from fastapi import FastAPI, Query
from typing import Annotated

app = FastAPI()

@app.get("/items/")
async def read_items(q: Annotated[list[str], Query()] = None):
    return {"q": q}
```

Accessing `/items/?q=a&q=b&q=c` returns `{"q": ["a", "b", "c"]}`

### Combining Path and Query Parameters

```python
@app.get("/users/{user_id}/items/")
async def read_user_items(
    user_id: int,
    skip: int = 0,
    limit: int = 10,
    q: str = None
):
    return {
        "user_id": user_id,
        "skip": skip,
        "limit": limit,
        "q": q
    }
```

---

## 10. Request Body and Data Validation {#request-body-and-data-validation}

### Pydantic Models

Pydantic provides data validation and serialization using Python type hints.

#### Basic Model Definition

```python
from pydantic import BaseModel

class Item(BaseModel):
    name: str
    description: str = None
    price: float
    tax: float = None
```

#### Using Models in FastAPI

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    name: str
    price: float

@app.post("/items/")
async def create_item(item: Item):
    return item
```

### Field Validation

#### Basic Field Constraints

```python
from pydantic import BaseModel, Field

class Item(BaseModel):
    name: str = Field(..., min_length=1, max_length=100)
    price: float = Field(..., gt=0, lt=1000000)
    quantity: int = Field(default=1, ge=0)
```

Field parameters:

- **min_length**: Minimum string length
- **max_length**: Maximum string length
- **pattern**: Regex pattern
- **gt**: Greater than
- **gte**: Greater than or equal
- **lt**: Less than
- **lte**: Less than or equal
- **multiple_of**: Must be multiple of value

#### Examples and Descriptions

```python
from pydantic import BaseModel, Field

class Item(BaseModel):
    name: str = Field(..., description="Item name", example="Widget")
    price: float = Field(..., description="Item price", example=9.99)
```

### Custom Validators

```python
from pydantic import BaseModel, field_validator

class Item(BaseModel):
    name: str
    price: float
    
    @field_validator('price')
    @classmethod
    def price_must_be_positive(cls, v):
        if v <= 0:
            raise ValueError('Price must be positive')
        return v
```

### Nested Models

```python
from pydantic import BaseModel

class Address(BaseModel):
    street: str
    city: str
    country: str

class User(BaseModel):
    name: str
    email: str
    address: Address
```

### Model Inheritance

```python
from pydantic import BaseModel

class ItemBase(BaseModel):
    name: str
    description: str = None

class ItemCreate(ItemBase):
    price: float

class Item(ItemBase):
    id: int
    price: float
```

### Arbitrary Type Validation

```python
from pydantic import BaseModel
from datetime import datetime

class Event(BaseModel):
    name: str
    timestamp: datetime
    
    model_config = {"arbitrary_types_allowed": True}
```

### Config and Model Settings

```python
from pydantic import BaseModel, ConfigDict

class Item(BaseModel):
    model_config = ConfigDict(
        json_schema_extra={"example": {"name": "Item", "price": 9.99}},
        validate_assignment=True,
    )
    
    name: str
    price: float
```

### Serialization Mode

```python
from pydantic import BaseModel
from datetime import datetime

class Event(BaseModel):
    name: str
    created_at: datetime

event = Event(name="Update", created_at="2024-01-01T00:00:00")
print(event.model_dump())  # Python objects
print(event.model_dump_json())  # JSON string
```

---

## 11. Response Models and Status Codes {#response-models-and-status-codes}

### Defining Response Models

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    id: int
    name: str
    price: float
    in_stock: bool = True

@app.get("/items/{item_id}", response_model=Item)
async def get_item(item_id: int):
    return {"id": item_id, "name": "Widget", "price": 9.99, "in_stock": True}
```

### Response Model Filtering

#### Excluding Fields

```python
@app.get("/items/{item_id}", response_model=Item, response_model_exclude={"price"})
async def get_item(item_id: int):
    return {"id": item_id, "name": "Widget", "price": 9.99, "in_stock": True}
```

#### Including Specific Fields

```python
@app.get("/items/{item_id}", response_model=Item, response_model_include={"id", "name"})
async def get_item(item_id: int):
    return {"id": item_id, "name": "Widget", "price": 9.99, "in_stock": True}
```

#### Excluding Defaults

```python
@app.get("/items/", response_model=Item, response_model_exclude_defaults=True)
async def get_items():
    return [{"id": 1, "name": "Widget", "price": 9.99}]
```

#### Excluding Unset Fields

```python
@app.get("/items/", response_model=Item, response_model_exclude_unset=True)
async def get_items():
    return [{"id": 1, "name": "Widget", "price": 9.99}]
```

### HTTP Status Codes

#### Specifying Status Codes

```python
from fastapi import FastAPI, status

app = FastAPI()

@app.post("/items/", status_code=status.HTTP_201_CREATED)
async def create_item(item: dict):
    return item
```

#### Status Code Constants

```python
from fastapi import status

# Success codes
status.HTTP_200_OK
status.HTTP_201_CREATED
status.HTTP_204_NO_CONTENT

# Client error codes
status.HTTP_400_BAD_REQUEST
status.HTTP_401_UNAUTHORIZED
status.HTTP_403_FORBIDDEN
status.HTTP_404_NOT_FOUND
status.HTTP_422_UNPROCESSABLE_ENTITY

# Server error codes
status.HTTP_500_INTERNAL_SERVER_ERROR
status.HTTP_503_SERVICE_UNAVAILABLE
```

### Multiple Response Models

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    name: str
    price: float

class ItemOut(BaseModel):
    id: int
    name: str
    price: float

@app.get("/items/{item_id}", response_model=ItemOut)
async def get_item(item_id: int):
    return {"id": item_id, "name": "Widget", "price": 9.99}
```

### Response Descriptions

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    name: str
    price: float

@app.get(
    "/items/",
    response_model=list[Item],
    responses={
        200: {"description": "Items retrieved successfully"},
        404: {"description": "No items found"}
    }
)
async def get_items():
    return []
```

---

## 12. Error Handling and Exception Management {#error-handling-and-exception-management}

### HTTPException

The standard way to return errors in FastAPI:

```python
from fastapi import FastAPI, HTTPException, status

app = FastAPI()

@app.get("/items/{item_id}")
async def read_item(item_id: int):
    if item_id == 0:
        raise HTTPException(
            status_code=status.HTTP_404_NOT_FOUND,
            detail="Item not found"
        )
    return {"item_id": item_id}
```

#### HTTPException Parameters

- **status_code**: HTTP status code to return
- **detail**: Detail message
- **headers**: Response headers

### Request Validation Errors

FastAPI automatically returns 422 Unprocessable Entity for validation errors:

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    name: str
    price: float

@app.post("/items/")
async def create_item(item: Item):
    return item
```

Invalid request automatically returns:
```json
{
    "detail": [
        {
            "loc": ["body", "price"],
            "msg": "value is not a valid number",
            "type": "type_error.number"
        }
    ]
}
```

### Custom Exception Handlers

#### Override Default Exception Handler

```python
from fastapi import FastAPI, Request
from fastapi.responses import JSONResponse

app = FastAPI()

class CustomException(Exception):
    def __init__(self, name: str):
        self.name = name

@app.exception_handler(CustomException)
async def custom_exception_handler(request: Request, exc: CustomException):
    return JSONResponse(
        status_code=400,
        content={"message": f"Custom error: {exc.name}"}
    )

@app.get("/items/")
async def read_items():
    raise CustomException(name="item_error")
```

#### Handle Request Validation Errors

```python
from fastapi import FastAPI, Request
from fastapi.exceptions import RequestValidationError
from fastapi.responses import JSONResponse

app = FastAPI()

@app.exception_handler(RequestValidationError)
async def validation_exception_handler(request: Request, exc: RequestValidationError):
    return JSONResponse(
        status_code=422,
        content={"detail": exc.errors()}
    )
```

### Error Response Format

#### Standardized Error Format

```python
from fastapi import FastAPI, HTTPException, status
from pydantic import BaseModel

app = FastAPI()

class ErrorResponse(BaseModel):
    error_code: str
    message: str
    details: dict = None

@app.get("/items/{item_id}")
async def read_item(item_id: int):
    if item_id < 0:
        raise HTTPException(
            status_code=status.HTTP_400_BAD_REQUEST,
            detail={
                "error_code": "INVALID_ID",
                "message": "Item ID must be positive"
            }
        )
    return {"item_id": item_id}
```

### Try-Except in Endpoints

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/items/{item_id}")
async def read_item(item_id: int):
    try:
        # Perform operations
        return {"item_id": item_id}
    except ValueError as e:
        return {"error": str(e)}, 400
    except Exception as e:
        return {"error": "Internal server error"}, 500
```

---

## 13. Middleware in FastAPI {#middleware-in-fastapi}

### What is Middleware?

Middleware is a function or class that processes requests before they reach the endpoint and processes responses before they are sent to the client.

### Basic Middleware

```python
from fastapi import FastAPI
from starlette.middleware.base import BaseHTTPMiddleware
from starlette.requests import Request

app = FastAPI()

class CustomMiddleware(BaseHTTPMiddleware):
    async def dispatch(self, request: Request, call_next):
        # Pre-processing
        print(f"Request path: {request.url.path}")
        
        # Forward to endpoint
        response = await call_next(request)
        
        # Post-processing
        response.headers["X-Process-Time"] = "0.5"
        return response

app.add_middleware(CustomMiddleware)
```

### Middleware Execution Order

Middleware added later executes first for requests but last for responses:

```python
app = FastAPI()

app.add_middleware(ThirdMiddleware)  # Executes 3rd on request
app.add_middleware(SecondMiddleware)  # Executes 2nd on request
app.add_middleware(FirstMiddleware)   # Executes 1st on request
```

### Common Middleware Examples

#### Logging Middleware

```python
from fastapi import FastAPI
from starlette.middleware.base import BaseHTTPMiddleware
from starlette.requests import Request
import time

app = FastAPI()

class LoggingMiddleware(BaseHTTPMiddleware):
    async def dispatch(self, request: Request, call_next):
        start_time = time.time()
        response = await call_next(request)
        process_time = time.time() - start_time
        response.headers["X-Process-Time"] = str(process_time)
        print(f"{request.method} {request.url.path} - {process_time}")
        return response

app.add_middleware(LoggingMiddleware)
```

#### Authentication Middleware

```python
from fastapi import FastAPI, HTTPException, status
from starlette.middleware.base import BaseHTTPMiddleware
from starlette.requests import Request

app = FastAPI()

class AuthMiddleware(BaseHTTPMiddleware):
    async def dispatch(self, request: Request, call_next):
        if not request.headers.get("authorization"):
            raise HTTPException(
                status_code=status.HTTP_401_UNAUTHORIZED,
                detail="Missing authorization header"
            )
        response = await call_next(request)
        return response

app.add_middleware(AuthMiddleware)
```

#### Request ID Middleware

```python
from fastapi import FastAPI
from starlette.middleware.base import BaseHTTPMiddleware
from starlette.requests import Request
import uuid

app = FastAPI()

class RequestIDMiddleware(BaseHTTPMiddleware):
    async def dispatch(self, request: Request, call_next):
        request_id = str(uuid.uuid4())
        request.scope["request_id"] = request_id
        response = await call_next(request)
        response.headers["X-Request-ID"] = request_id
        return response

app.add_middleware(RequestIDMiddleware)
```

### Using Starlette Middleware

#### CORS Middleware

```python
from fastapi import FastAPI
from starlette.middleware.cors import CORSMiddleware

app = FastAPI()

app.add_middleware(
    CORSMiddleware,
    allow_origins=["http://localhost:3000", "https://example.com"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)
```

#### TrustedHost Middleware

```python
from fastapi import FastAPI
from starlette.middleware.trustedhost import TrustedHostMiddleware

app = FastAPI()

app.add_middleware(
    TrustedHostMiddleware,
    allowed_hosts=["example.com", "*.example.com"]
)
```

#### GZIP Middleware

```python
from fastapi import FastAPI
from starlette.middleware.gzip import GZIPMiddleware

app = FastAPI()

app.add_middleware(GZIPMiddleware, minimum_size=1000)
```

---

## 14. CORS and Security Headers {#cors-and-security-headers}

### Understanding CORS

CORS (Cross-Origin Resource Sharing) is a security mechanism that allows restricted resources on a web page to be requested from another domain.

#### CORS Problem

By default, browsers block requests from one domain to another for security reasons.

**Example**:
- Frontend running on `http://localhost:3000`
- Backend running on `http://localhost:8000`
- Direct requests from frontend to backend will be blocked

### Implementing CORS in FastAPI

#### Simple CORS Configuration

```python
from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware

app = FastAPI()

app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],  # Allow all origins
    allow_credentials=True,
    allow_methods=["*"],  # Allow all HTTP methods
    allow_headers=["*"],  # Allow all headers
)

@app.get("/items/")
async def read_items():
    return [{"name": "Item 1"}]
```

#### Specific Origins CORS

```python
from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware

app = FastAPI()

app.add_middleware(
    CORSMiddleware,
    allow_origins=[
        "http://localhost",
        "http://localhost:3000",
        "https://example.com"
    ],
    allow_credentials=True,
    allow_methods=["GET", "POST"],
    allow_headers=["*"],
)
```

#### CORS Parameters Explained

- **allow_origins**: List of allowed origin domains
- **allow_credentials**: Allow cookies and authentication headers
- **allow_methods**: List of allowed HTTP methods
- **allow_headers**: List of allowed headers
- **expose_headers**: Headers exposed to browser
- **max_age**: Browser cache time for CORS response

### Security Headers

Security headers protect against common web vulnerabilities.

#### Implementing Security Headers via Middleware

```python
from fastapi import FastAPI
from starlette.middleware.base import BaseHTTPMiddleware
from starlette.requests import Request

app = FastAPI()

class SecurityHeadersMiddleware(BaseHTTPMiddleware):
    async def dispatch(self, request: Request, call_next):
        response = await call_next(request)
        response.headers["X-Content-Type-Options"] = "nosniff"
        response.headers["X-Frame-Options"] = "DENY"
        response.headers["X-XSS-Protection"] = "1; mode=block"
        response.headers["Strict-Transport-Security"] = "max-age=31536000; includeSubDomains"
        response.headers["Content-Security-Policy"] = "default-src 'self'"
        return response

app.add_middleware(SecurityHeadersMiddleware)
```

#### Important Security Headers

| Header | Purpose | Value |
|--------|---------|-------|
| X-Content-Type-Options | Prevent MIME type sniffing | nosniff |
| X-Frame-Options | Clickjacking protection | DENY, SAMEORIGIN |
| X-XSS-Protection | XSS attack protection | 1; mode=block |
| Strict-Transport-Security | Force HTTPS | max-age=31536000 |
| Content-Security-Policy | Control resource loading | default-src 'self' |

### Combined CORS and Security

```python
from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware
from starlette.middleware.base import BaseHTTPMiddleware
from starlette.requests import Request

app = FastAPI()

# CORS Middleware
app.add_middleware(
    CORSMiddleware,
    allow_origins=["http://localhost:3000"],
    allow_credentials=True,
    allow_methods=["GET", "POST"],
    allow_headers=["*"],
)

# Security Headers Middleware
class SecurityHeadersMiddleware(BaseHTTPMiddleware):
    async def dispatch(self, request: Request, call_next):
        response = await call_next(request)
        response.headers["X-Content-Type-Options"] = "nosniff"
        response.headers["X-Frame-Options"] = "DENY"
        return response

app.add_middleware(SecurityHeadersMiddleware)
```

---

## 15. Authentication and Authorization {#authentication-and-authorization}

### Authentication vs Authorization

- **Authentication**: Verifying the identity of a user
- **Authorization**: Determining what an authenticated user is allowed to do

### Basic Authentication

Basic Auth sends credentials in a Base64-encoded format in the Authorization header.

```python
from fastapi import FastAPI, Depends, HTTPException, status
from fastapi.security import HTTPBasic, HTTPBasicCredentials

app = FastAPI()
security = HTTPBasic()

def verify_credentials(credentials: HTTPBasicCredentials = Depends(security)):
    username = "admin"
    password = "secret"
    
    if credentials.username != username or credentials.password != password:
        raise HTTPException(
            status_code=status.HTTP_401_UNAUTHORIZED,
            detail="Invalid credentials",
            headers={"WWW-Authenticate": "Basic"},
        )
    return credentials.username

@app.get("/protected/")
async def protected_route(username: str = Depends(verify_credentials)):
    return {"message": f"Hello {username}"}
```

### API Key Authentication

API keys are simple tokens sent in headers or query parameters.

```python
from fastapi import FastAPI, Depends, HTTPException, status
from fastapi.security import APIKeyHeader

app = FastAPI()

api_key_header = APIKeyHeader(name="X-API-Key")

async def verify_api_key(api_key: str = Depends(api_key_header)):
    if api_key != "your-secret-api-key":
        raise HTTPException(
            status_code=status.HTTP_401_UNAUTHORIZED,
            detail="Invalid API key"
        )
    return api_key

@app.get("/protected/")
async def protected_route(api_key: str = Depends(verify_api_key)):
    return {"message": "Access granted"}
```

### Bearer Token Authentication

Bearer tokens are typically JWT tokens sent in the Authorization header.

```python
from fastapi import FastAPI, Depends, HTTPException, status
from fastapi.security import HTTPBearer, HTTPAuthCredentials

app = FastAPI()
bearer = HTTPBearer()

async def verify_bearer(credentials: HTTPAuthCredentials = Depends(bearer)):
    token = credentials.credentials
    if token != "valid-token":
        raise HTTPException(
            status_code=status.HTTP_401_UNAUTHORIZED,
            detail="Invalid token"
        )
    return token

@app.get("/protected/")
async def protected_route(token: str = Depends(verify_bearer)):
    return {"message": "Access granted"}
```

### Role-Based Authorization

```python
from fastapi import FastAPI, Depends, HTTPException, status
from fastapi.security import HTTPBearer, HTTPAuthCredentials

app = FastAPI()
bearer = HTTPBearer()

def get_current_user(credentials: HTTPAuthCredentials = Depends(HTTPBearer())):
    # Extract and validate token
    return {"username": "user", "role": "admin"}

def require_admin(current_user = Depends(get_current_user)):
    if current_user.get("role") != "admin":
        raise HTTPException(
            status_code=status.HTTP_403_FORBIDDEN,
            detail="Insufficient permissions"
        )
    return current_user

@app.delete("/users/{user_id}")
async def delete_user(user_id: int, admin: dict = Depends(require_admin)):
    return {"message": f"User {user_id} deleted by {admin['username']}"}
```

---

## 16. JWT Token Implementation {#jwt-token-implementation}

### What are JWT Tokens?

JWT (JSON Web Token) is a stateless authentication token consisting of three parts: header, payload, and signature.

### JWT Structure

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJ1c2VybmFtZSIsImV4cCI6MTY3MTAwMDAwMH0.signature
```

- **Header**: Token type and hashing algorithm
- **Payload**: Claims (user data)
- **Signature**: Encoded header and payload signed with secret

### Installing JWT Library

```bash
pip install python-jose passlib
```

### Creating JWT Tokens

```python
from datetime import datetime, timedelta
from jose import jwt

SECRET_KEY = "your-secret-key-change-in-production"
ALGORITHM = "HS256"

def create_access_token(data: dict, expires_delta: timedelta = None):
    to_encode = data.copy()
    if expires_delta:
        expire = datetime.utcnow() + expires_delta
    else:
        expire = datetime.utcnow() + timedelta(hours=1)
    
    to_encode.update({"exp": expire})
    encoded_jwt = jwt.encode(to_encode, SECRET_KEY, algorithm=ALGORITHM)
    return encoded_jwt
```

### Verifying JWT Tokens

```python
from jose import JWTError, jwt
from fastapi import HTTPException, status

SECRET_KEY = "your-secret-key"
ALGORITHM = "HS256"

async def verify_token(token: str):
    try:
        payload = jwt.decode(token, SECRET_KEY, algorithms=[ALGORITHM])
        username: str = payload.get("sub")
        if username is None:
            raise HTTPException(
                status_code=status.HTTP_401_UNAUTHORIZED,
                detail="Invalid token"
            )
        return username
    except JWTError:
        raise HTTPException(
            status_code=status.HTTP_401_UNAUTHORIZED,
            detail="Invalid token"
        )
```

### Complete JWT Authentication Flow

```python
from fastapi import FastAPI, Depends, HTTPException, status
from fastapi.security import HTTPBearer, HTTPAuthCredentials
from datetime import datetime, timedelta
from jose import jwt, JWTError
from pydantic import BaseModel

app = FastAPI()
bearer = HTTPBearer()

SECRET_KEY = "your-secret-key"
ALGORITHM = "HS256"

class Token(BaseModel):
    access_token: str
    token_type: str

class User(BaseModel):
    username: str
    email: str

def create_access_token(data: dict):
    to_encode = data.copy()
    expire = datetime.utcnow() + timedelta(hours=24)
    to_encode.update({"exp": expire})
    encoded_jwt = jwt.encode(to_encode, SECRET_KEY, algorithm=ALGORITHM)
    return encoded_jwt

def verify_token(credentials: HTTPAuthCredentials = Depends(bearer)):
    token = credentials.credentials
    try:
        payload = jwt.decode(token, SECRET_KEY, algorithms=[ALGORITHM])
        username: str = payload.get("sub")
        if username is None:
            raise HTTPException(status_code=401, detail="Invalid token")
        return username
    except JWTError:
        raise HTTPException(status_code=401, detail="Invalid token")

@app.post("/login/", response_model=Token)
async def login(username: str, password: str):
    # Verify credentials (simplified)
    if username == "user" and password == "password":
        access_token = create_access_token({"sub": username})
        return {"access_token": access_token, "token_type": "bearer"}
    raise HTTPException(status_code=401, detail="Invalid credentials")

@app.get("/users/me", response_model=User)
async def get_current_user(username: str = Depends(verify_token)):
    return {"username": username, "email": f"{username}@example.com"}
```

---

## 17. OAuth2 Integration {#oauth2-integration}

### Understanding OAuth2

OAuth2 is an authorization framework that enables applications to obtain limited access to user accounts on an HTTP service.

### OAuth2 Flow

1. User clicks "Login with Provider"
2. User is redirected to provider's login page
3. User logs in and authorizes the application
4. Provider redirects back with authorization code
5. Application exchanges code for access token
6. Application uses access token to access user data

### OAuth2 with FastAPI

```python
from fastapi import FastAPI, Depends, HTTPException, status
from fastapi.security import OAuth2PasswordBearer, OAuth2PasswordRequestForm
from pydantic import BaseModel

app = FastAPI()

oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")

class User(BaseModel):
    username: str
    email: str = None
    full_name: str = None

def get_current_user(token: str = Depends(oauth2_scheme)):
    # Verify token and return user
    return {"username": "user"}

@app.post("/token/")
async def login(form_data: OAuth2PasswordRequestForm = Depends()):
    # Authenticate user
    return {"access_token": "token", "token_type": "bearer"}

@app.get("/users/me", response_model=User)
async def read_users_me(current_user = Depends(get_current_user)):
    return current_user
```

### Google OAuth2 Integration

```python
from fastapi import FastAPI
from fastapi_oauth2 import OAuth2

app = FastAPI()

oauth2 = OAuth2(
    client_id="your-client-id",
    client_secret="your-client-secret",
    redirect_uri="http://localhost:8000/callback"
)

@app.get("/login/")
async def login():
    return {"url": oauth2.get_authorization_url()}

@app.get("/callback/")
async def callback(code: str):
    token = await oauth2.get_access_token(code)
    return {"token": token}
```

---

## 18. File Upload and Download Management {#file-upload-and-download-management}

### File Upload

#### Single File Upload

```python
from fastapi import FastAPI, File, UploadFile

app = FastAPI()

@app.post("/upload/")
async def upload_file(file: UploadFile = File(...)):
    contents = await file.read()
    return {
        "filename": file.filename,
        "size": len(contents),
        "content_type": file.content_type
    }
```

#### Multiple File Upload

```python
from fastapi import FastAPI, File, UploadFile
from typing import list

app = FastAPI()

@app.post("/upload-multiple/")
async def upload_multiple_files(files: list[UploadFile] = File(...)):
    return [
        {
            "filename": file.filename,
            "content_type": file.content_type
        }
        for file in files
    ]
```

#### Save File to Disk

```python
from fastapi import FastAPI, File, UploadFile
import shutil

app = FastAPI()

@app.post("/upload/")
async def upload_file(file: UploadFile = File(...)):
    with open(f"uploads/{file.filename}", "wb") as buffer:
        shutil.copyfileobj(file.file, buffer)
    return {"filename": file.filename}
```

#### File Upload with Form Data

```python
from fastapi import FastAPI, File, Form, UploadFile

app = FastAPI()

@app.post("/upload/")
async def upload_file(
    file: UploadFile = File(...),
    description: str = Form(...)
):
    return {
        "filename": file.filename,
        "description": description
    }
```

### File Download

#### Download File

```python
from fastapi import FastAPI
from fastapi.responses import FileResponse
import os

app = FastAPI()

@app.get("/download/{filename}")
async def download_file(filename: str):
    file_path = f"uploads/{filename}"
    if not os.path.exists(file_path):
        return {"error": "File not found"}
    
    return FileResponse(
        path=file_path,
        filename=filename,
        media_type="application/octet-stream"
    )
```

#### Stream File Download

```python
from fastapi import FastAPI
from fastapi.responses import StreamingResponse
import os

app = FastAPI()

@app.get("/download/{filename}")
async def download_file(filename: str):
    file_path = f"uploads/{filename}"
    
    def iterfile():
        with open(file_path, "rb") as f:
            yield from f
    
    return StreamingResponse(
        iterfile(),
        media_type="application/octet-stream",
        headers={"Content-Disposition": f"attachment; filename={filename}"}
    )
```

---

## 19. WebSocket Communication {#websocket-communication}

### Understanding WebSocket

WebSocket provides full-duplex communication over a single TCP connection, enabling real-time bidirectional communication between client and server.

### WebSocket Lifecycle

1. Client initiates WebSocket connection
2. Server accepts connection
3. Bidirectional communication occurs
4. Either party can close the connection

### Basic WebSocket Connection

```python
from fastapi import FastAPI, WebSocket

app = FastAPI()

@app.websocket("/ws")
async def websocket_endpoint(websocket: WebSocket):
    await websocket.accept()
    try:
        while True:
            data = await websocket.receive_text()
            await websocket.send_text(f"Echo: {data}")
    except Exception as e:
        print(f"Error: {e}")
    finally:
        await websocket.close()
```

### WebSocket with Multiple Connections

```python
from fastapi import FastAPI, WebSocket
from fastapi.websocket import WebSocketDisconnect

app = FastAPI()

class ConnectionManager:
    def __init__(self):
        self.active_connections = []
    
    async def connect(self, websocket: WebSocket):
        await websocket.accept()
        self.active_connections.append(websocket)
    
    def disconnect(self, websocket: WebSocket):
        self.active_connections.remove(websocket)
    
    async def broadcast(self, message: str):
        for connection in self.active_connections:
            await connection.send_text(message)

manager = ConnectionManager()

@app.websocket("/ws/{client_id}")
async def websocket_endpoint(websocket: WebSocket, client_id: int):
    await manager.connect(websocket)
    try:
        while True:
            data = await websocket.receive_text()
            await manager.broadcast(f"Client {client_id}: {data}")
    except WebSocketDisconnect:
        manager.disconnect(websocket)
        await manager.broadcast(f"Client {client_id} is offline")
```

### WebSocket with JSON Data

```python
from fastapi import FastAPI, WebSocket
from fastapi.websocket import WebSocketDisconnect
from pydantic import BaseModel

app = FastAPI()

class Message(BaseModel):
    type: str
    content: str

@app.websocket("/ws")
async def websocket_endpoint(websocket: WebSocket):
    await websocket.accept()
    try:
        while True:
            data = await websocket.receive_json()
            message = Message(**data)
            await websocket.send_json({"echo": message.content})
    except WebSocketDisconnect:
        print("Client disconnected")
```

### WebSocket Authentication

```python
from fastapi import FastAPI, WebSocket, status
from fastapi.websocket import WebSocketDisconnect

app = FastAPI()

@app.websocket("/ws")
async def websocket_endpoint(websocket: WebSocket):
    # Check authorization header
    headers = dict(websocket.headers)
    token = headers.get("authorization")
    
    if not token or not verify_token(token):
        await websocket.close(code=status.WS_1008_POLICY_VIOLATION)
        return
    
    await websocket.accept()
    try:
        while True:
            data = await websocket.receive_text()
            await websocket.send_text(f"Echo: {data}")
    except WebSocketDisconnect:
        print("Client disconnected")
```

---

## 20. RESTful API Design Principles {#restful-api-design-principles}

### What is REST?

REST (Representational State Transfer) is an architecture style for designing web APIs that use HTTP methods and URLs to represent resources and operations.

### Core Principles of REST

#### 1. Client-Server Architecture

- Client and server are separate concerns
- Client depends on URLs and contracts
- Server implementation can change independently

#### 2. Statelessness

- Each request contains all information needed
- Server doesn't store client context
- Simplifies server design and improves scalability

#### 3. Uniform Interface

- Resources are identified by URIs
- Resources are manipulated through representations
- Self-descriptive messages
- HATEOAS (Hypermedia As The Engine Of Application State)

#### 4. Cacheability

- Responses should define themselves as cacheable or not
- Reduces latency and improves performance

#### 5. Layered System

- Client cannot tell if connected directly to end server
- Allows for scalability and security layers

#### 6. Code on Demand (Optional)

- Server can extend client functionality by transferring code

### Resource-Oriented Design

Resources are the core abstraction in REST. Design endpoints around nouns, not verbs.

#### Good Resource URLs

```
GET    /api/users                    # Get all users
GET    /api/users/{id}               # Get specific user
POST   /api/users                    # Create new user
PUT    /api/users/{id}               # Replace user
PATCH  /api/users/{id}               # Update user
DELETE /api/users/{id}               # Delete user
```

#### Bad Resource URLs (Verb-Based)

```
GET    /api/getUsers                 # Avoid verbs
POST   /api/createUser               # Use HTTP methods instead
GET    /api/deleteUser?id=1          # Don't use query params for operations
```

### HTTP Methods and Expected Behavior

| Method | Purpose | Idempotent | Safe | Example |
|--------|---------|-----------|------|---------|
| GET | Retrieve resource | Yes | Yes | GET /users/1 |
| POST | Create resource | No | No | POST /users |
| PUT | Replace resource | Yes | No | PUT /users/1 |
| PATCH | Partial update | No* | No | PATCH /users/1 |
| DELETE | Remove resource | Yes | No | DELETE /users/1 |

### Status Codes for REST APIs

#### Success Responses

- **200 OK**: Standard success response
- **201 Created**: Resource successfully created
- **204 No Content**: Successful request with no response body

#### Client Error Responses

- **400 Bad Request**: Invalid request format
- **401 Unauthorized**: Authentication required
- **403 Forbidden**: Authenticated but access denied
- **404 Not Found**: Resource not found
- **422 Unprocessable Entity**: Validation error

#### Server Error Responses

- **500 Internal Server Error**: Unexpected server error
- **503 Service Unavailable**: Server temporarily unavailable

### RESTful API Example

```python
from fastapi import FastAPI, HTTPException, status
from pydantic import BaseModel

app = FastAPI()

class User(BaseModel):
    id: int = None
    name: str
    email: str

users = []

@app.get("/api/users", response_model=list[User])
async def list_users():
    return users

@app.post("/api/users", response_model=User, status_code=status.HTTP_201_CREATED)
async def create_user(user: User):
    user.id = len(users) + 1
    users.append(user)
    return user

@app.get("/api/users/{user_id}", response_model=User)
async def get_user(user_id: int):
    for user in users:
        if user.id == user_id:
            return user
    raise HTTPException(status_code=404, detail="User not found")

@app.put("/api/users/{user_id}", response_model=User)
async def update_user(user_id: int, updated_user: User):
    for i, user in enumerate(users):
        if user.id == user_id:
            updated_user.id = user_id
            users[i] = updated_user
            return updated_user
    raise HTTPException(status_code=404, detail="User not found")

@app.patch("/api/users/{user_id}", response_model=User)
async def partial_update_user(user_id: int, user_data: dict):
    for user in users:
        if user.id == user_id:
            if "name" in user_data:
                user.name = user_data["name"]
            if "email" in user_data:
                user.email = user_data["email"]
            return user
    raise HTTPException(status_code=404, detail="User not found")

@app.delete("/api/users/{user_id}", status_code=status.HTTP_204_NO_CONTENT)
async def delete_user(user_id: int):
    for i, user in enumerate(users):
        if user.id == user_id:
            users.pop(i)
            return None
    raise HTTPException(status_code=404, detail="User not found")
```

---

## 21. Database Integration with FastAPI {#database-integration-with-fastapi}

### Database Options for FastAPI

#### SQL Databases

- **PostgreSQL**: Robust, feature-rich relational database
- **MySQL**: Popular open-source relational database
- **SQLite**: Lightweight, file-based database

#### NoSQL Databases

- **MongoDB**: Document-based, flexible schema
- **Redis**: In-memory, key-value store
- **Cassandra**: Distributed, wide-column store

### Connection Basics

#### SQLite Connection

```python
import sqlite3

def get_db():
    conn = sqlite3.connect("database.db")
    conn.row_factory = sqlite3.Row
    try:
        yield conn
    finally:
        conn.close()
```

#### PostgreSQL Connection

```python
import psycopg2

def get_db():
    conn = psycopg2.connect(
        host="localhost",
        database="mydb",
        user="user",
        password="password"
    )
    try:
        yield conn
    finally:
        conn.close()
```

### Using Database with FastAPI Endpoint

```python
from fastapi import FastAPI, Depends
import sqlite3

app = FastAPI()

def get_db():
    conn = sqlite3.connect("database.db")
    try:
        yield conn
    finally:
        conn.close()

@app.get("/users/")
async def get_users(db = Depends(get_db)):
    cursor = db.cursor()
    cursor.execute("SELECT * FROM users")
    users = cursor.fetchall()
    return users
```

---

## 22. SQLAlchemy ORM Integration {#sqlalchemy-orm-integration}

### What is SQLAlchemy?

SQLAlchemy is a Python SQL toolkit and Object-Relational Mapping (ORM) library that abstracts database operations.

### Installation

```bash
pip install sqlalchemy
```

### Creating Database Models

```python
from sqlalchemy import Column, Integer, String, create_engine
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker

DATABASE_URL = "sqlite:///./test.db"

engine = create_engine(DATABASE_URL, connect_args={"check_same_thread": False})
SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)
Base = declarative_base()

class User(Base):
    __tablename__ = "users"
    
    id = Column(Integer, primary_key=True, index=True)
    name = Column(String, index=True)
    email = Column(String, unique=True, index=True)

Base.metadata.create_all(bind=engine)
```

### CRUD Operations with SQLAlchemy

```python
from fastapi import FastAPI, Depends
from sqlalchemy.orm import Session
from pydantic import BaseModel

app = FastAPI()

class UserCreate(BaseModel):
    name: str
    email: str

class UserResponse(BaseModel):
    id: int
    name: str
    email: str
    
    class Config:
        from_attributes = True

def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()

@app.post("/users/", response_model=UserResponse)
async def create_user(user: UserCreate, db: Session = Depends(get_db)):
    db_user = User(name=user.name, email=user.email)
    db.add(db_user)
    db.commit()
    db.refresh(db_user)
    return db_user

@app.get("/users/{user_id}", response_model=UserResponse)
async def get_user(user_id: int, db: Session = Depends(get_db)):
    return db.query(User).filter(User.id == user_id).first()

@app.get("/users/", response_model=list[UserResponse])
async def list_users(db: Session = Depends(get_db)):
    return db.query(User).all()

@app.put("/users/{user_id}", response_model=UserResponse)
async def update_user(user_id: int, user: UserCreate, db: Session = Depends(get_db)):
    db_user = db.query(User).filter(User.id == user_id).first()
    db_user.name = user.name
    db_user.email = user.email
    db.commit()
    db.refresh(db_user)
    return db_user

@app.delete("/users/{user_id}")
async def delete_user(user_id: int, db: Session = Depends(get_db)):
    db_user = db.query(User).filter(User.id == user_id).first()
    db.delete(db_user)
    db.commit()
    return {"message": "User deleted"}
```

### Relationships in SQLAlchemy

```python
from sqlalchemy import ForeignKey
from sqlalchemy.orm import relationship

class User(Base):
    __tablename__ = "users"
    
    id = Column(Integer, primary_key=True)
    name = Column(String)
    posts = relationship("Post", back_populates="author")

class Post(Base):
    __tablename__ = "posts"
    
    id = Column(Integer, primary_key=True)
    title = Column(String)
    user_id = Column(Integer, ForeignKey("users.id"))
    author = relationship("User", back_populates="posts")
```

---

## 23. Async and Await in FastAPI {#async-and-await-in-fastapi}

### Understanding Async Programming

Async programming allows a single thread to handle multiple I/O operations concurrently without blocking.

### Async Functions in FastAPI

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/items/")
async def read_items():
    return {"items": ["item1", "item2"]}
```

The `async` keyword indicates that the function is asynchronous.

### Using Await

The `await` keyword pauses execution until an async operation completes.

```python
import asyncio
from fastapi import FastAPI

app = FastAPI()

async def get_data():
    await asyncio.sleep(1)
    return {"data": "value"}

@app.get("/data/")
async def read_data():
    result = await get_data()
    return result
```

### Async Database Operations

```python
from fastapi import FastAPI, Depends
from sqlalchemy.ext.asyncio import AsyncSession, create_async_engine
from sqlalchemy.orm import sessionmaker

DATABASE_URL = "sqlite+aiosqlite:///./test.db"

engine = create_async_engine(DATABASE_URL)
AsyncSessionLocal = sessionmaker(engine, class_=AsyncSession, expire_on_commit=False)

async def get_db():
    async with AsyncSessionLocal() as session:
        yield session

@app.get("/users/")
async def list_users(db: AsyncSession = Depends(get_db)):
    result = await db.execute("SELECT * FROM users")
    return result.fetchall()
```

### Concurrent Requests

FastAPI automatically handles concurrent requests using async:

```python
import asyncio
from fastapi import FastAPI

app = FastAPI()

async def get_user(user_id: int):
    await asyncio.sleep(1)
    return {"id": user_id, "name": "User"}

@app.get("/users/{user_id}")
async def read_user(user_id: int):
    return await get_user(user_id)
```

Multiple concurrent requests are handled efficiently without blocking.

### TaskGroup for Concurrent Operations (Python 3.11+)

```python
import asyncio
from fastapi import FastAPI

app = FastAPI()

@app.get("/data/")
async def read_data():
    async def fetch_users():
        await asyncio.sleep(1)
        return {"users": []}
    
    async def fetch_items():
        await asyncio.sleep(1)
        return {"items": []}
    
    async with asyncio.TaskGroup() as tg:
        users_task = tg.create_task(fetch_users())
        items_task = tg.create_task(fetch_items())
    
    return {
        "users": users_task.result(),
        "items": items_task.result()
    }
```

---

## 24. Dependency Injection System {#dependency-injection-system}

### What is Dependency Injection?

Dependency Injection (DI) is a design pattern that enables a class to receive its dependencies from external sources rather than creating them itself.

### FastAPI Dependency System

FastAPI has a built-in dependency injection system using the `Depends` function.

### Basic Dependencies

```python
from fastapi import FastAPI, Depends

def get_query(q: str = None):
    return q

app = FastAPI()

@app.get("/items/")
async def read_items(q: str = Depends(get_query)):
    return {"q": q}
```

### Classes as Dependencies

```python
from fastapi import FastAPI, Depends

class CommonQueryParams:
    def __init__(self, skip: int = 0, limit: int = 10):
        self.skip = skip
        self.limit = limit

app = FastAPI()

@app.get("/items/")
async def read_items(commons: CommonQueryParams = Depends()):
    return {"skip": commons.skip, "limit": commons.limit}
```

### Nested Dependencies

```python
from fastapi import FastAPI, Depends

def get_skip(skip: int = 0):
    return skip

def get_limit(limit: int = 10):
    return limit

def get_query(skip: int = Depends(get_skip), limit: int = Depends(get_limit)):
    return {"skip": skip, "limit": limit}

app = FastAPI()

@app.get("/items/")
async def read_items(query: dict = Depends(get_query)):
    return query
```

### Global Dependencies

```python
from fastapi import FastAPI, Depends

def verify_token(token: str):
    if not token:
        raise Exception("Invalid token")
    return token

app = FastAPI(dependencies=[Depends(verify_token)])

@app.get("/items/")
async def read_items():
    return {"items": []}
```

### Dependency Caching

Dependencies are executed once per request unless configured otherwise:

```python
from fastapi import FastAPI, Depends

call_count = 0

def expensive_operation():
    global call_count
    call_count += 1
    return call_count

app = FastAPI()

@app.get("/items/")
async def read_items(first: int = Depends(expensive_operation), second: int = Depends(expensive_operation)):
    return {"first": first, "second": second}
```

Both `first` and `second` receive the same value because of caching.

---

## 25. Testing FastAPI Applications {#testing-fastapi-applications}

### Installation

```bash
pip install pytest httpx pytest-asyncio
```

### Basic Test Structure

```python
from fastapi import FastAPI
from fastapi.testclient import TestClient

app = FastAPI()

@app.get("/items/")
async def read_items():
    return {"items": ["item1", "item2"]}

client = TestClient(app)

def test_read_items():
    response = client.get("/items/")
    assert response.status_code == 200
    assert response.json() == {"items": ["item1", "item2"]}
```

### Testing Endpoints with Pytest

```python
import pytest
from fastapi.testclient import TestClient
from main import app

client = TestClient(app)

def test_get_items():
    response = client.get("/api/items/")
    assert response.status_code == 200

def test_create_item():
    response = client.post(
        "/api/items/",
        json={"name": "Widget", "price": 9.99}
    )
    assert response.status_code == 201

def test_get_item_not_found():
    response = client.get("/api/items/9999")
    assert response.status_code == 404
```

### Testing with Dependencies

```python
from fastapi import Depends, FastAPI
from fastapi.testclient import TestClient

app = FastAPI()

def get_db():
    return {"db": "connection"}

@app.get("/users/")
async def get_users(db = Depends(get_db)):
    return {"users": []}

client = TestClient(app)

def test_get_users():
    response = client.get("/users/")
    assert response.status_code == 200

def test_with_override():
    def override_get_db():
        return {"db": "test"}
    
    app.dependency_overrides[get_db] = override_get_db
    response = client.get("/users/")
    assert response.status_code == 200
    app.dependency_overrides.clear()
```

### Testing Authentication

```python
from fastapi import FastAPI, Depends, HTTPException
from fastapi.security import HTTPBearer
from fastapi.testclient import TestClient

app = FastAPI()
bearer = HTTPBearer()

def verify_token(credentials = Depends(bearer)):
    if credentials.credentials != "valid-token":
        raise HTTPException(status_code=401)
    return credentials.credentials

@app.get("/protected/")
async def protected(token = Depends(verify_token)):
    return {"message": "Success"}

client = TestClient(app)

def test_without_token():
    response = client.get("/protected/")
    assert response.status_code == 403

def test_with_invalid_token():
    response = client.get(
        "/protected/",
        headers={"Authorization": "Bearer invalid"}
    )
    assert response.status_code == 401

def test_with_valid_token():
    response = client.get(
        "/protected/",
        headers={"Authorization": "Bearer valid-token"}
    )
    assert response.status_code == 200
```

---

## 26. Example Projects {#example-projects}

### Project 1: Simple Todo API

```python
from fastapi import FastAPI, HTTPException, status
from pydantic import BaseModel
from typing import List

app = FastAPI(title="Todo API")

class TodoCreate(BaseModel):
    title: str
    description: str = None
    completed: bool = False

class Todo(TodoCreate):
    id: int

todos = []

@app.post("/todos/", response_model=Todo, status_code=status.HTTP_201_CREATED)
async def create_todo(todo: TodoCreate):
    new_todo = Todo(**todo.dict(), id=len(todos) + 1)
    todos.append(new_todo)
    return new_todo

@app.get("/todos/", response_model=List[Todo])
async def list_todos():
    return todos

@app.get("/todos/{todo_id}", response_model=Todo)
async def get_todo(todo_id: int):
    for todo in todos:
        if todo.id == todo_id:
            return todo
    raise HTTPException(status_code=404, detail="Todo not found")

@app.put("/todos/{todo_id}", response_model=Todo)
async def update_todo(todo_id: int, updated_todo: TodoCreate):
    for todo in todos:
        if todo.id == todo_id:
            for key, value in updated_todo.dict().items():
                setattr(todo, key, value)
            return todo
    raise HTTPException(status_code=404, detail="Todo not found")

@app.delete("/todos/{todo_id}", status_code=status.HTTP_204_NO_CONTENT)
async def delete_todo(todo_id: int):
    for i, todo in enumerate(todos):
        if todo.id == todo_id:
            todos.pop(i)
            return None
    raise HTTPException(status_code=404, detail="Todo not found")
```

### Project 2: User Management with Authentication

```python
from fastapi import FastAPI, Depends, HTTPException, status
from fastapi.security import HTTPBasic, HTTPBasicCredentials
from pydantic import BaseModel
from typing import List

app = FastAPI(title="User Management API")
security = HTTPBasic()

class UserCreate(BaseModel):
    username: str
    password: str
    email: str

class User(BaseModel):
    id: int
    username: str
    email: str

users = []

def verify_credentials(credentials: HTTPBasicCredentials = Depends(security)):
    for user in users:
        if user["username"] == credentials.username and user["password"] == credentials.password:
            return user["username"]
    raise HTTPException(
        status_code=status.HTTP_401_UNAUTHORIZED,
        detail="Invalid credentials"
    )

@app.post("/register/", response_model=User, status_code=status.HTTP_201_CREATED)
async def register_user(user: UserCreate):
    new_user = {
        "id": len(users) + 1,
        "username": user.username,
        "password": user.password,
        "email": user.email
    }
    users.append(new_user)
    return User(**new_user)

@app.get("/users/me", response_model=User)
async def get_current_user(username: str = Depends(verify_credentials)):
    for user in users:
        if user["username"] == username:
            return User(**user)
    raise HTTPException(status_code=404, detail="User not found")

@app.get("/users/", response_model=List[User])
async def list_users(username: str = Depends(verify_credentials)):
    return [User(**u) for u in users]
```

---

## 27. Best Practices and Performance Optimization {#best-practices-and-performance-optimization}

### Code Organization

#### Project Structure

```
fastapi_project/
├── main.py
├── app/
│   ├── __init__.py
│   ├── api/
│   │   ├── __init__.py
│   │   └── endpoints/
│   │       ├── users.py
│   │       ├── items.py
│   ├── core/
│   │   ├── config.py
│   │   ├── security.py
│   ├── db/
│   │   └── models.py
│   └── models/
│       ├── user.py
│       ├── item.py
├── tests/
│   ├── test_api.py
│   ├── test_users.py
└── requirements.txt
```

### Performance Optimization

#### Using Response Model Efficiently

```python
# Good: Exclude unnecessary fields
@app.get("/users/", response_model=UserOut, response_model_exclude_unset=True)
async def list_users():
    return users

# Bad: Returning all fields even if not needed
@app.get("/users/")
async def list_users():
    return users  # May include sensitive fields
```

#### Connection Pooling

```python
from sqlalchemy.pool import NullPool
from sqlalchemy import create_engine

engine = create_engine(
    DATABASE_URL,
    poolclass=NullPool,  # Better for async
    echo=False
)
```

#### Caching

```python
from functools import lru_cache
from fastapi import FastAPI

app = FastAPI()

@lru_cache(maxsize=128)
def get_expensive_data():
    # Expensive computation
    return {"data": "value"}

@app.get("/data/")
async def read_data():
    return get_expensive_data()
```

### Security Best Practices

#### HTTPS in Production

Always use HTTPS in production.

#### Environment Variables

```python
from fastapi import FastAPI
import os

SECRET_KEY = os.getenv("SECRET_KEY")
DATABASE_URL = os.getenv("DATABASE_URL")
```

#### Input Validation

Always validate inputs with Pydantic models.

#### SQL Injection Prevention

Always use parameterized queries with SQLAlchemy or ORM.

### Error Handling Best Practices

```python
from fastapi import FastAPI, HTTPException, status
import logging

app = FastAPI()
logger = logging.getLogger(__name__)

@app.get("/items/{item_id}")
async def read_item(item_id: int):
    try:
        # Operation
        return {"item_id": item_id}
    except ValueError as e:
        logger.error(f"Invalid value: {e}")
        raise HTTPException(
            status_code=status.HTTP_400_BAD_REQUEST,
            detail="Invalid item ID"
        )
    except Exception as e:
        logger.exception("Unexpected error")
        raise HTTPException(
            status_code=status.HTTP_500_INTERNAL_SERVER_ERROR,
            detail="Internal server error"
        )
```

### Documentation Best Practices

```python
from fastapi import FastAPI

app = FastAPI(
    title="My API",
    description="Complete API description",
    version="1.0.0",
)

@app.get("/items/{item_id}")
async def read_item(item_id: int):
    """
    Get an item by ID.
    
    - **item_id**: The ID of the item (must be positive)
    
    Returns the item with the specified ID.
    """
    return {"item_id": item_id}
```

---

## 28. Deployment and Production Considerations {#deployment-and-production-considerations}

### Development vs Production

#### Development Server

```bash
uvicorn main:app --reload
```

Used only for development with hot reloading.

#### Production Server

Use production-grade ASGI servers:

- Uvicorn with Gunicorn
- Hypercorn
- Daphne

### Gunicorn + Uvicorn Setup

```bash
pip install gunicorn

gunicorn main:app -w 4 -k uvicorn.workers.UvicornWorker
```

**Parameters**:
- `-w 4`: Number of worker processes
- `-k`: Worker class

### Docker Deployment

#### Dockerfile

```dockerfile
FROM python:3.9

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

#### Building and Running

```bash
docker build -t fastapi_app .
docker run -p 8000:8000 fastapi_app
```

### Environment Configuration

```python
from pydantic_settings import BaseSettings

class Settings(BaseSettings):
    app_name: str = "FastAPI App"
    debug: bool = False
    database_url: str
    secret_key: str
    
    class Config:
        env_file = ".env"

settings = Settings()
```

### Health Check Endpoint

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/health/")
async def health_check():
    return {"status": "ok"}
```

### Logging Configuration

```python
import logging

logging.basicConfig(
    level=logging.INFO,
    format="%(asctime)s - %(name)s - %(levelname)s - %(message)s"
)

logger = logging.getLogger(__name__)

logger.info("Application started")
```

---

## 29. Real-World Use Cases {#real-world-use-cases}

### E-commerce API

Building an API for product catalog, shopping cart, and orders.

### Social Media Backend

User authentication, post creation, likes, comments, and notifications.

### IoT Data Collection

Receiving sensor data from devices and storing in database.

### Real-time Chat Application

WebSocket-based chat with multiple users.

### Analytics Dashboard

Collecting and aggregating data for visualization.

### Microservices Architecture

Building multiple FastAPI services that communicate with each other.

---

## 30. Troubleshooting and Common Issues {#troubleshooting-and-common-issues}

### Issue: CORS Errors

**Problem**: Requests from frontend blocked.

**Solution**:
```python
from fastapi.middleware.cors import CORSMiddleware

app.add_middleware(
    CORSMiddleware,
    allow_origins=["http://localhost:3000"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)
```

### Issue: Validation Errors (422)

**Problem**: Request data fails validation.

**Solution**: Check request body against Pydantic model definitions.

### Issue: Database Connection Errors

**Problem**: Cannot connect to database.

**Solution**:
- Verify database URL
- Check credentials
- Ensure database is running
- Test connection separately

### Issue: Slow Response Times

**Problem**: API responses are slow.

**Solution**:
- Use async operations
- Implement caching
- Optimize database queries
- Use connection pooling
- Profile with tools like cProfile

### Issue: Memory Leaks

**Problem**: Memory usage continuously increases.

**Solution**:
- Properly close database connections
- Clear caches periodically
- Use context managers
- Monitor with tools

### Issue: WebSocket Connection Issues

**Problem**: WebSocket connections not working.

**Solution**:
- Ensure endpoint is defined with `@app.websocket()`
- Check that client is connecting to correct path
- Verify authentication if required
- Check browser console for errors

---

## 31. Additional Resources and References {#additional-resources-and-references}

### Official Documentation

- **FastAPI Documentation**: https://fastapi.tiangolo.com/
- **Pydantic Documentation**: https://docs.pydantic.dev/
- **Starlette Documentation**: https://www.starlette.io/
- **SQLAlchemy Documentation**: https://docs.sqlalchemy.org/

### Learning Resources

- **Real Python - FastAPI Tutorials**: https://realpython.com/
- **FreeCodeCamp - FastAPI Course**: https://freecodecamp.org/
- **Udemy FastAPI Courses**: https://udemy.com/
- **FastAPI GitHub Repository**: https://github.com/tiangolo/fastapi

### Tools and Libraries

- **HTTPie**: Command-line HTTP client
- **Postman**: API testing and documentation tool
- **Thunder Client**: VS Code API testing extension
- **curl**: Command-line HTTP client

### Related Concepts

- **REST API Design**: Design patterns for APIs
- **GraphQL**: Alternative to REST for APIs
- **gRPC**: High-performance RPC framework
- **Message Queues**: Asynchronous task processing (Celery, RQ)
- **Microservices**: Architecture pattern

### HTTP and Network Concepts

- **HTTP Status Codes**: Understanding response codes
- **HTTP Headers**: Metadata headers and their purpose
- **TCP/IP**: Transport and internet protocols
- **DNS**: Domain name resolution

### Python Concepts

- **Async/Await**: Asynchronous programming in Python
- **Decorators**: Function modification and enhancement
- **Context Managers**: Resource management with `with` statement
- **Type Hints**: Python typing system

---

## Conclusion

This comprehensive guide covers network programming using Python with FastAPI at the Application Layer. FastAPI provides a modern, efficient, and user-friendly framework for building robust web APIs that can handle various network communication patterns from simple HTTP requests to real-time WebSocket connections.

Key takeaways:

1. **FastAPI is Application Layer Focused**: Works exclusively with HTTP/HTTPS and WebSocket protocols
2. **Modern Python Features**: Leverages type hints, async/await, and Pydantic for clean, maintainable code
3. **Developer Experience**: Automatic documentation, validation, and serialization reduce boilerplate
4. **Production Ready**: Can be deployed to production with proper configuration and security measures
5. **Extensible**: Middleware, dependencies, and plugins enable customization and scalability

By mastering FastAPI, you have the tools to build professional, scalable network applications that serve web clients, mobile apps, IoT devices, and other service consumers efficiently.

---

**Document Version**: 1.0
**Last Updated**: April 2026
**Author**: Comprehensive Network Programming Guide
