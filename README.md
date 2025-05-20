# Flask + MySQL Dockerized Application

This project is a simple Flask web application that connects to a MySQL database and displays the MySQL version. It's containerized using Docker and built in two stages for a smaller final image size.

## Features

- Flask web app
- Connects to a MySQL database using `mysqlclient`
- Docker multi-stage build for optimized image size
- Runs on port `5002`

## Prerequisites

- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/) (recommended for multi-container setup)

## Project Structure
.
├── app.py # Main Flask application
├── Dockerfile # Docker multi-stage build file
└── README.md # Project documentation

## Running the App

This application expects a MySQL database to be running and accessible. It's recommended to use **Docker Compose** to run both the Flask app and the MySQL container.

### Step 1: Create a `docker-compose.yml` file

```yaml
version: '3.8'

services:
  mydb:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: my-secret-pw
      MYSQL_DATABASE: flaskdb
    ports:
      - "3306:3306"

  flask-app:
    build: .
    ports:
      - "5002:5002"
    depends_on:
      - mydb

**Step 2: Build and Start the Containers
**
  docker-compose up --build

**Step 3: Access the App
**
  Open your browser and navigate to: http://localhost:5002
  
  You should see output similar to:
  
  Hello, World! MySQL version: 5.7.x

**Notes**

    The Flask app connects to the MySQL container using the hostname mydb (as defined in Docker Compose).

    Ensure the mysqlclient Python package is compatible with your Python and MySQL versions.

**Stopping the App
**
  Press Ctrl+C in the terminal running Docker Compose, then run:

docker-compose down
