# Go Movies CRUD API

[![Go Version](https://img.shields.io/badge/Go-1.26.3-00ADD8?style=for-the-badge&logo=go)](https://golang.org/)
[![Gorilla Mux](https://img.shields.io/badge/Router-Gorilla%20Mux-F6851B?style=for-the-badge&logo=go)](https://github.com/gorilla/mux)
[![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge)](#)

A sleek, robust, and lightning-fast RESTful CRUD API built in Go using the `gorilla/mux` router. It manages an in-memory database of movies, complete with directors, and supports all standard CRUD operations.

---

## 📐 Architecture & API Flow

The routing mechanism uses the `gorilla/mux` router to direct incoming requests to their respective handler functions.

```mermaid
flowchart LR
    %% Left Server Section
    subgraph Server_Section["Server & Data"]
        direction TB
        DB[("DATABASE")]
        Cross["✕ (No DB / In-Memory Only)"]
        Server["MOVIES SERVER<br>(LOCALHOST:8000)"]
        
        DB -.-> Cross -.-> Server
    end
    
    %% Router Distribution
    Server -->|GORILLA MUX| R1
    Server --> R2
    Server --> R3
    Server --> R4
    Server --> R5

    subgraph API_Grid["Routing Matrix (Routes ➔ Functions ➔ Endpoints ➔ Methods)"]
        direction TB
        
        subgraph Row1["Get All Movies"]
            R1["GET ALL"] ───► F1["getMovies"] ───► E1["/movies"] ───► M1["GET"]
        end
        
        subgraph Row2["Get Movie by ID"]
            R2["GET BY ID"] ───► F2["getMovie"] ───► E2["/movies/{id}"] ───► M2["GET"]
        end
        
        subgraph Row3["Create Movie"]
            R3["CREATE"] ───► F3["createMovie"] ───► E3["/movies"] ───► M3["POST"]
        end
        
        subgraph Row4["Update Movie"]
            R4["UPDATE"] ───► F4["updateMovie"] ───► E4["/movies/{id}"] ───► M4["PUT"]
        end
        
        subgraph Row5["Delete Movie"]
            R5["DELETE"] ───► F5["deleteMovie"] ───► E5["/movies/{id}"] ───► M5["DELETE"]
        end
    end

    %% Styles
    classDef server fill:#0f172a,stroke:#38bdf8,stroke-width:2px,color:#fff;
    classDef route fill:#1e293b,stroke:#94a3b8,stroke-width:1px,color:#e2e8f0;
    classDef fn fill:#3b82f6,stroke:#1d4ed8,stroke-width:1px,color:#fff;
    classDef endpoint fill:#10b981,stroke:#047857,stroke-width:1px,color:#fff;
    classDef method fill:#8b5cf6,stroke:#6d28d9,stroke-width:1px,color:#fff;
    classDef db fill:#dc2626,stroke:#991b1b,stroke-width:1px,color:#fff;
    
    class Server server;
    class DB db;
    class R1,R2,R3,R4,R5 route;
    class F1,F2,F3,F4,F5 fn;
    class E1,E2,E3,E4,E5 endpoint;
    class M1,M2,M3,M4,M5 method;
```

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
