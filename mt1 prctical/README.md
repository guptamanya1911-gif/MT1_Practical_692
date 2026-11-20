# Products REST API — Backend Mid-Term 1 Practical

A clean, beginner-friendly RESTful API built with **Node.js** and **Express.js** for managing product inventory using an in-memory JavaScript array.

---

## Technologies Used

- **Node.js** — JavaScript runtime environment
- **Express.js** — Web framework for building REST APIs
- **JavaScript (ES6+)** — Core programming language
- **In-Memory Array** — Lightweight data storage without external databases

---

## Installation Instructions

1. Clone the repository:
   ```bash
   git clone https://github.com/lakshmiinteriors786786-dotcom/MT1-FSD-Practical.git
   ```

2. Navigate to the project folder:
   ```bash
   cd "MT1-FSD-Practical/mt1 prctical"
   ```

3. Install dependencies:
   ```bash
   npm install
   ```

---

## How to Start the Server

Run the following command to start the application on port `3000`:

```bash
npm start
```

The server will start at:
```
http://localhost:3000
```

To run the automated test suite:
```bash
npm test
```

---

## Product Data Schema

Each product stored in the in-memory array has the following structure:

| Field      | Type   | Description                         |
| ---------- | ------ | ----------------------------------- |
| `id`       | Number | Auto-generated unique numeric ID    |
| `name`     | String | Product name (must be unique)       |
| `price`    | Number | Product price (positive number)     |
| `category` | String | Product category                    |

---

## API Endpoints

| Method   | Endpoint                     | Description                                      |
| -------- | ---------------------------- | ------------------------------------------------ |
| `POST`   | `/api/products`              | Add a new product (auto-generates ID)            |
| `GET`    | `/api/products`              | Retrieve all products (supports `?category=...`) |
| `GET`    | `/api/products/:id`          | Retrieve a single product by ID                  |
| `PUT`    | `/api/products/:id`          | Update an existing product by ID                 |
| `DELETE` | `/api/products/:id`          | Delete a product by ID                           |

---

## Example JSON Request Bodies & Responses

### 1. Create a New Product (`POST /api/products`)

**Request Body:**
```json
{
  "name": "Bluetooth Headphones",
  "price": 59.99,
  "category": "Electronics"
}
```

**Success Response (`201 Created`):**
```json
{
  "id": 4,
  "name": "Bluetooth Headphones",
  "price": 59.99,
  "category": "Electronics"
}
```

---

### 2. Get All Products (`GET /api/products`)

**Success Response (`200 OK`):**
```json
[
  {
    "id": 1,
    "name": "Wireless Mouse",
    "price": 25.99,
    "category": "Electronics"
  },
  {
    "id": 2,
    "name": "Mechanical Keyboard",
    "price": 79.99,
    "category": "Electronics"
  },
  {
    "id": 3,
    "name": "Coffee Mug",
    "price": 12.5,
    "category": "Kitchen"
  }
]
```

---

### 3. Category Filtering (`GET /api/products?category=Electronics`)

Filter products by category using the `category` query parameter (`req.query.category`).

**Request:**
```http
GET /api/products?category=Electronics
```

**Success Response (`200 OK`):**
```json
[
  {
    "id": 1,
    "name": "Wireless Mouse",
    "price": 25.99,
    "category": "Electronics"
  },
  {
    "id": 2,
    "name": "Mechanical Keyboard",
    "price": 79.99,
    "category": "Electronics"
  }
]
```

---

### 4. Get a Product by ID (`GET /api/products/:id`)

**Request:**
```http
GET /api/products/1
```

**Success Response (`200 OK`):**
```json
{
  "id": 1,
  "name": "Wireless Mouse",
  "price": 25.99,
  "category": "Electronics"
}
```

---

### 5. Update an Existing Product (`PUT /api/products/:id`)

**Request:**
```http
PUT /api/products/1
```

**Request Body:**
```json
{
  "name": "Ergonomic Wireless Mouse",
  "price": 29.99,
  "category": "Electronics"
}
```

**Success Response (`200 OK`):**
```json
{
  "id": 1,
  "name": "Ergonomic Wireless Mouse",
  "price": 29.99,
  "category": "Electronics"
}
```

---

### 6. Delete a Product (`DELETE /api/products/:id`)

**Request:**
```http
DELETE /api/products/3
```

**Success Response (`200 OK`):**
```json
{
  "message": "Product deleted successfully.",
  "product": {
    "id": 3,
    "name": "Coffee Mug",
    "price": 12.5,
    "category": "Kitchen"
  }
}
```

---

## Expected HTTP Status Codes

| Status Code         | Condition                                                                 |
| ------------------- | ------------------------------------------------------------------------- |
| `200 OK`            | Successful `GET`, `PUT`, or `DELETE` request                              |
| `201 Created`       | Product successfully created via `POST /api/products`                     |
| `400 Bad Request`   | Missing or invalid required fields (`name`, `price`, or `category`)       |
| `404 Not Found`     | Product with the specified `:id` does not exist or ID is invalid          |
| `409 Conflict`      | Duplicate product name detected on creation (`POST`) or update (`PUT`)    |
