# Go Movies CRUD API

[![Go Version](https://img.shields.io/badge/Go-1.26.3-00ADD8?style=for-the-badge&logo=go)](https://golang.org/)
[![Gorilla Mux](https://img.shields.io/badge/Router-Gorilla%20Mux-F6851B?style=for-the-badge&logo=go)](https://github.com/gorilla/mux)
[![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge)](#)

A sleek, robust, and lightning-fast RESTful CRUD API built in Go using the `gorilla/mux` router. It manages an in-memory database of movies, complete with directors, and supports all standard CRUD operationss.

---

## 📐 Architecture & API Flow

The routing mechanism uses the `gorilla/mux` router to direct incoming requests to their respective handler functions.

---

## ⚡ Features

- **No External Database Overhead**: Currently runs an in-memory data store using Go slices—designed for extreme speed.
- **RESTful Endpoints**: Clean HTTP mapping (GET, POST, PUT, DELETE).
- **Type-Safe Models**: Fully structured models representing `Movie` and `Director` entities.
- **Auto-generated IDs**: Automatically assigns random identifiers to newly created movies.

---

## 🛠️ Getting Started

### Prerequisites

Make sure you have [Go](https://go.dev/doc/install) installed (version 1.16+ recommended).

### Running the Server

1. Clone or navigate to the repository directory.
2. Initialize dependencies and run:
   ```bash
   go run main.go
   ```
3. The server will start spinning at: `http://localhost:8000`

---

## 🚀 API Endpoint Documentation & Testing

### 1. Get All Movies
* **Endpoint**: `GET /movies`
* **Handler**: `getMovies`
* **Test**:
  ```bash
  curl http://localhost:8000/movies
  ```

### 2. Get Movie by ID
* **Endpoint**: `GET /movies/{id}`
* **Handler**: `getMovie`
* **Test**:
  ```bash
  curl http://localhost:8000/movies/1
  ```

### 3. Create Movie
* **Endpoint**: `POST /movies`
* **Handler**: `createMovie`
* **Test**:
  ```bash
  curl -X POST -H "Content-Type: application/json" -d '{
    "isbn": "987654",
    "title": "Interstellar",
    "director": {
      "firstname": "Christopher",
      "lastname": "Nolan"
    }
  }' http://localhost:8000/movies
  ```

### 4. Update Movie
* **Endpoint**: `PUT /movies/{id}`
* **Handler**: `updateMovie`
* **Test**:
  ```bash
  curl -X PUT -H "Content-Type: application/json" -d '{
    "isbn": "438227",
    "title": "Dhurandhar (Extended Cut)",
    "director": {
      "firstname": "Mukesh",
      "lastname": "Bhatt"
    }
  }' http://localhost:8000/movies/1
  ```

### 5. Delete Movie
* **Endpoint**: `DELETE /movies/{id}`
* **Handler**: `deleteMovie`
* **Test**:
  ```bash
  curl -X DELETE http://localhost:8000/movies/2
  ```

---

## 📂 Project Structure

```text
├── go.mod        # Go module specification
├── go.sum        # Module lock file
├── main.go       # Core server & route handler logic
└── README.md     # Project documentation & architecture diagram
```
