# Go SQL Server

This is a simple HTTP server written in Go that interacts with a MySQL database to manage a collection of albums. The server provides RESTful endpoints to create, read, update, and delete albums.

## Prerequisites

- Go 1.22.4 or later
- MySQL server
- `go-sql-driver/mysql` package
- `gorilla/mux` package

## Setup

1. **Clone the repository**:
    ```sh
    git clone https://github.com/alex1092/records-go-crud-server
    cd go-sql-server
    ```

2. **Install dependencies**:
    Ensure you have Go installed. If not, download and install it from the [official Go website](https://golang.org/dl/).

    Then, run:
    ```sh
    go mod tidy
    ```

3. **Set up the MySQL database**:
    - Start your MySQL server.
    - Create a database named `recordings`:
        ```sql
        CREATE DATABASE recordings;
        ```
    - Create a table named `album`:
        ```sql
        USE recordings;
        CREATE TABLE album (
            id INT AUTO_INCREMENT,
            title VARCHAR(100),
            artist VARCHAR(100),
            price DECIMAL(10, 2),
            PRIMARY KEY (id)
        );
        ```

4. **Configure the database connection**:
    Update the `connectDB` function in `main.go` with your MySQL user and password:
    ```go
    cfg := mysql.Config{
        User:   "your_mysql_user",
        Passwd: "your_mysql_password",
        Net:    "tcp",
        Addr:   "127.0.0.1:3306",
        DBName: "recordings",
    }
    ```

5. **Run the server**:
    ```sh
    go run main.go
    ```

    The server will start on `http://localhost:8080`.

6. **Test the endpoints**:
    You can use tools like `curl` or Postman to test the RESTful endpoints:
    - **Create an album**:
        ```sh
        curl -X POST -H "Content-Type: application/json" -d '{"title":"Album Title","artist":"Artist Name","price":9.99}' http://localhost:8080/albums
        ```
    - **Get all albums**:
        ```sh
        curl http://localhost:8080/albums
        ```
    - **Get an album by ID**:
        ```sh
        curl http://localhost:8080/albums/1
        ```
    - **Update an album**:
        ```sh
        curl -X PUT -H "Content-Type: application/json" -d '{"title":"New Title","artist":"New Artist","price":19.99}' http://localhost:8080/albums/1
        ```
    - **Delete an album**:
        ```sh
        curl -X DELETE http://localhost:8080/albums/1
        ```
