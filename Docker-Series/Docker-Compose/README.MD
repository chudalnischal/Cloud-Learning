# Docker Compose for Beginners

Docker Compose is a tool used to define and manage multi-container Docker applications using a simple YAML configuration file. It allows developers to run multiple services (like databases, backends, and frontends) easily with a single command.

## What is Docker Compose?

Docker Compose is a tool for defining and running multi-container Docker applications. With a YAML file, you can configure your application’s services, networks, and volumes. It simplifies the management of complex applications involving multiple containers.

**Key Features of Docker Compose:**

- **Multi-Container Management:** Manage multiple containers with one command.

- **Networking: Automatically** sets up a network for your containers to communicate.

- **Volume Management:** Provides persistent storage using Docker volumes.

- **Environment Management:** Pass environment variables to containers.

### Prerequisites

Before getting started, ensure you have the following installed:

- Docker
- Docker Compose (included with Docker Desktop)

You can verify installations using:
```bash
docker --version
docker-compose --version
``` 

### Step 1: Understanding Docker Compose

A docker-compose.yml file is used to define services, networks, and volumes.

Example Structure
```bash
project-directory/
├── docker-compose.yml
└── app/
    ├── Dockerfile
    ├── app.py
    ├── requirements.txt
```

### Step 2: Creating a Simple Application with Flask and MongoDB

We will create a simple Python web application using Flask and MongoDB using Docker Compose.

**app.py**
```python
from flask import Flask, jsonify
from pymongo import MongoClient

app = Flask(__name__)
client = MongoClient('mongodb://mongo:27017/')
db = client['testdb']
collection = db['testcollection']

@app.route('/')
def home():
    return "Hello, Docker Compose with Flask and MongoDB!"

@app.route('/data')
def get_data():
    data = list(collection.find({}, {'_id': 0}))
    return jsonify(data)

if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0')
```

**requirements.txt**
```bash
flask
pymongo
```

**Dockerfile**
```yaml
# Use an official Python runtime as a parent image
FROM python:3.11-slim

# Set the working directory
WORKDIR /app

# Copy the application files
COPY requirements.txt ./
COPY app.py ./

# Install dependencies
RUN pip install -r requirements.txt

# Expose the application port
EXPOSE 5000

# Run the application
CMD ["python", "app.py"]
```

### Step 3: Writing the Docker Compose File

Create a docker-compose.yml file with the following content:
```yaml
version: '3.8'

services:
  web:
    build: ./app
    ports:
      - "5000:5000"
    volumes:
      - ./app:/app
    environment:
      - FLASK_ENV=development
    depends_on:
      - mongo

  mongo:
    image: mongo:latest
    ports:
      - "27017:27017"
    volumes:
      - mongodb_data:/data/db

volumes:
  mongodb_data:
```

Explanation
- version: Specifies the Docker Compose file format.
- services: Defines the containers to be managed.
- web: The name of the service (Flask application).
- build: Path to the Dockerfile.
- ports: Maps port 5000 on the host to port 5000 in the container.
- volumes: Mounts the application directory to the container to allow code changes without rebuilding.
- environment: Passes environment variables to the container.
- depends_on: Ensures the MongoDB container starts before the Flask container.
- mongo: The name of the MongoDB service.
- image: Uses the official MongoDB image from Docker Hub.
- ports: Maps MongoDB’s default port 27017.
- volumes: Stores persistent database data using Docker volumes.
- volumes: Defines a persistent volume (mongodb_data) to ensure MongoDB data is not lost when the container stops.

### Step 4: Running the Application

Navigate to the directory containing the docker-compose.yml file and run:
```bash
docker-compose up
```
The up command builds the images (if necessary) and starts the containers.

Access the application by navigating to http://localhost:5000 in your browser.
Access database data using the /data endpoint at http://localhost:5000/data.

To stop the application, run:
```bash
docker-compose down
```

Additional Tips

Rebuild Container: If you change the Dockerfile, run:
```bash
docker-compose up --build
```

View Logs:
```bash
docker-compose logs
```

Check Container Status:
```bash
docker-compose ps
```

## Conclusion

You have successfully created a Docker Compose setup to run a Flask web application with MongoDB. Docker Compose is a powerful tool for managing multi-container applications and simplifies the development process.

For further learning, check the official Docker Compose documentation: https://docs.docker.com/compose/

Happy Dockering! 🚀

