 # Toronto Time API
 
This is a simple API built using Go that provides the current time in Toronto (adjusted for its time zone) in JSON format. Each request to the API is logged into a MySQL database, capturing the timestamp.

## Features

-Exposes an API endpoint /current-time that returns the current time in Toronto in JSON format.

-Logs each API request timestamp into a MySQL database (time_log table).

## Prerequisites

-Go: Ensure you have Go installed on your system. Download Go

-Docker (optional): If you prefer to run MySQL in a Docker container instead of installing it locally.

-MySQL Database: A running MySQL instance is required to store the API logs.

## Setup Instructions

## Step 1: MySQL Setup

-Using Docker: Run the following command to start a MySQL container:

"docker run --name mysql-container -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=toronto_time -p 3306:3306 -d mysql:latest"

This will create a database named toronto_time and set the root password to root.

Manual MySQL Setup:

Install MySQL on your system and create a database named toronto_time:

"CREATE DATABASE toronto_time;"

Create a table time_log inside the toronto_time database:

"USE toronto_time;
CREATE TABLE time_log (
    id INT AUTO_INCREMENT PRIMARY KEY,
    timestamp DATETIME NOT NULL
);"

## Step 2: Clone the Repository

Clone the repository or copy the Go code into a project directory:


git clone https://github.com/your-username/toronto-time-api.git
cd toronto-time-api

## Step 3: Install Dependencies

Install the required Go packages using the following command:

"go mod tidy"

## Step 4: Update Database Configuration

Ensure the database connection string in the Go code matches your MySQL setup. Update the following line in main.go if necessary:

"db, err = sql.Open("mysql", "root:root@tcp(127.0.0.1:3306)/toronto_time")"

Replace root:root with your MySQL username and password.

Ensure the 127.0.0.1:3306 address matches your MySQL host and port.

## Step 5: Run the Application

Start the Go application:

"go run main.go"

## Using the API

Open a browser or a tool like Postman, and make a GET request to:

http://localhost:8080/current-time

Verify Database Logging: Log in to your MySQL database and check the time_log table:

"SELECT * FROM time_log;"

## Error Handling

If the application cannot connect to the database, it will panic during startup.

If the /current-time endpoint fails to retrieve Toronto time, it will return a 500 Internal Server Error.

## Folder Structure

.
├── main.go        # Main Go file containing the API logic

├── go.mod         # Go modules file

├── README.md      # Documentation file

## Dependencies

-Go-SQL-Driver for MySQL: MySQL driver for Go.

-net/http: For creating the web server.

-time: For handling Toronto timezone adjustments.

-encoding/json: For JSON response formatting.

