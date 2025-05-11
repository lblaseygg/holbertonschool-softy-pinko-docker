# Softy Pinko Docker Project

This project demonstrates the implementation of a web application using Docker containers, featuring a front-end, back-end, and proxy server. The application is built in multiple stages, each adding new functionality and complexity.

## Project Structure

The project is organized into multiple tasks, each building upon the previous one:

- `task0/`: Basic Docker image that echoes "Hello, World!"
- `task1/`: Back-end Flask server with a simple API endpoint
- `task2/`: Front-end static server using Nginx
- `task3/`: Connected front-end and back-end with CORS support
- `task4/`: Docker Compose setup for service orchestration
- `task5/`: Added proxy server for request routing
- `task6/`: Horizontal scaling with multiple back-end instances

## Prerequisites

- Docker
- Docker Compose
- Git

## Setup and Running

### Task 0: Basic Docker Image
```bash
cd task0
docker build -f ./Dockerfile -t softy-pinko:task0 .
docker run -it --rm --name softy-pinko-task0 softy-pinko:task0
```

### Task 1: Back-end Server
```bash
cd task1
docker build -f ./Dockerfile -t softy-pinko:task1 .
docker run -p 5252:5252 -it --rm --name softy-pinko-task1 softy-pinko:task1
```

### Task 2: Front-end Server
```bash
cd task2
docker build -f ./front-end/Dockerfile -t softy-pinko-front-end:task2 ./front-end
docker run -p 9000:9000 -it --rm --name softy-pinko-front-end-task2 softy-pinko-front-end:task2
```

### Task 3: Connected Front-end and Back-end
```bash
cd task3
# Run back-end
docker build -f ./back-end/Dockerfile -t softy-pinko-back-end:task3 ./back-end
docker run -p 5252:5252 -it --rm --name softy-pinko-back-end-task3 softy-pinko-back-end:task3

# In another terminal, run front-end
docker build -f ./front-end/Dockerfile -t softy-pinko-front-end:task3 ./front-end
docker run -p 9000:9000 -it --rm --name softy-pinko-front-end-task3 softy-pinko-front-end:task3
```

### Task 4: Docker Compose Setup
```bash
cd task4
docker-compose build
docker-compose up
```

### Task 5: Proxy Server Setup
```bash
cd task5
docker-compose build
docker-compose up
```

### Task 6: Horizontal Scaling
```bash
cd task6
docker-compose build
docker-compose up --scale back-end=2
```

## Accessing the Application

- Task 0: No web access, outputs to terminal
- Task 1: API available at http://localhost:5252/api/hello
- Task 2: Front-end available at http://localhost:9000
- Task 3: 
  - Front-end: http://localhost:9000
  - Back-end: http://localhost:5252/api/hello
- Task 4: Same as Task 3 but using Docker Compose
- Task 5: All traffic routed through proxy at http://localhost
- Task 6: Same as Task 5 but with load-balanced back-end instances

## Architecture

### Task 5 & 6 Architecture
```
Client -> Proxy (Nginx) -> Front-end (Nginx) / Back-end (Flask)
```

The proxy server (port 80) routes requests to either:
- Front-end server (port 9000) for static content
- Back-end server (port 5252) for API requests

## Features

- Containerized application components
- Nginx for static file serving and reverse proxy
- Flask back-end with CORS support
- Docker Compose for service orchestration
- Horizontal scaling capability
- Load balancing between multiple back-end instances

## Notes

- The front-end is a static website served by Nginx
- The back-end is a Flask application providing a simple API
- CORS is enabled to allow cross-origin requests
- The proxy server handles all incoming traffic and routes it appropriately
- Task 6 demonstrates horizontal scaling with multiple back-end instances 