# Golang Database Learning

This repository contains examples of database operations in Go (Golang) using MySQL. It serves as a learning resource for understanding how to interact with databases in Go applications.

## 📋 Contents

- [Overview](#overview)
- [Project Structure](#project-structure)
- [Features](#features)
- [Setup](#setup)
- [Code Explanation](#code-explanation)
- [Key Concepts](#key-concepts)

## 🚀 Overview

This repository demonstrates how to connect a Go application with MySQL database using the `database/sql` package. It includes basic CRUD operations and concepts like prepared statements, transactions, and repository pattern. The code examples are written in a test-driven approach to demonstrate each concept individually.

## 📁 Project Structure

```
belajar-golang-database/
├── entity/
│   └── comment.go       # Data model for comment table
├── repository/
│   └── comment_repo.go  # Repository pattern implementation
├── app.go               # Main configuration file
├── database_test.go     # Database connection tests
├── query_parameter_test.go # Parameter query tests
├── repository_test.go   # Repository tests
├── sql_test.go          # Basic SQL tests
├── time_test.go         # Time data type tests
├── transaction_test.go  # Transaction tests
├── go.mod               # Module declaration and dependencies
└── go.sum               # Dependencies checksum
```

## ✨ Features

- MySQL database connection
- CRUD operations (Create, Read, Update, Delete)
- Prepared Statements for safe query execution
- Transactions for ensuring data consistency
- Repository Pattern for clean separation of concerns
- Unit Testing for all database operations

## 📝 Setup

### Prerequisites

- Go (version 1.16+)
- MySQL Server
- Git

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/fathirarya/belajar-golang-database.git
   ```

2. Install dependencies:
   ```bash
   go mod tidy
   ```

3. Set up MySQL database:
   ```sql
   CREATE DATABASE belajar_golang_database;
   USE belajar_golang_database;
   
   CREATE TABLE comments (
     id INT NOT NULL AUTO_INCREMENT,
     email VARCHAR(100) NOT NULL,
     comment TEXT,
     PRIMARY KEY (id)
   );
   ```

4. Update database connection in `app.go`:
   ```go
   db, err := sql.Open("mysql", "username:password@tcp(localhost:3306)/belajar_golang_database")
   ```

5. Run tests:
   ```bash
   go test -v ./...
   ```

## 🧩 Code Explanation

### Database Connection
```go
// database_test.go
db, err := sql.Open("mysql", "username:password@tcp(localhost:3306)/belajar_golang_database")
```
The code above establishes a connection to the MySQL database using the Go SQL driver.

### Entity Model
```go
// entity/comment.go
type Comment struct {
    Id      int
    Email   string
    Comment string
}
```
This struct represents the data structure that maps to the `comments` table in the database.

### Repository Pattern
```go
// repository/comment_repo.go
type CommentRepository interface {
    Insert(comment entity.Comment) (entity.Comment, error)
    FindById(id int) (entity.Comment, error)
    FindAll() ([]entity.Comment, error)
    // other methods...
}
```
The repository pattern provides an abstraction layer between the application and the database, making code more maintainable and testable.

### Prepared Statements
```go
// sql_test.go
stmt, err := db.Prepare("INSERT INTO comments(email, comment) VALUES(?, ?)")
result, err := stmt.Exec("email@example.com", "New comment")
```
Prepared statements help prevent SQL injection attacks by separating SQL logic from the data being inserted.

### Transactions
```go
// transaction_test.go
tx, err := db.Begin()
// Database operations
err = tx.Commit() // or tx.Rollback() on error
```
Transactions ensure that a series of database operations either all succeed or all fail, maintaining data integrity.

## 🔑 Key Concepts

- **Database Connection Pool**: Go's `database/sql` package manages a connection pool for efficient database operations.
- **Parameter Binding**: Using parameterized queries to safely handle user input.
- **Error Handling**: Proper error handling is demonstrated throughout the codebase.
- **Data Mapping**: Converting between Go structs and database records.
- **Testing**: Each database concept has corresponding test cases to verify functionality.

This repository provides a solid foundation for working with databases in Go applications, following best practices for secure and efficient data handling.