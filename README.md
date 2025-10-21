# Docker Learning - Node.js MongoDB Application

A containerized web application demonstrating Docker and Docker Compose with Node.js, Express, MongoDB, and Mongo Express.

## Overview

This project is a user profile management application that showcases how to:
- Containerize a Node.js application with Docker
- Use Docker Compose to orchestrate multiple services
- Connect a Node.js app to MongoDB
- Manage data persistence with Docker volumes
- Access MongoDB through Mongo Express web interface

## Tech Stack

- **Node.js** - Runtime environment
- **Express** - Web framework
- **MongoDB** - NoSQL database
- **Mongo Express** - Web-based MongoDB admin interface
- **Docker** - Containerization
- **Docker Compose** - Multi-container orchestration

## Project Structure

```
.
├── app/
│   ├── Dockerfile          # Docker image configuration
│   ├── server.js           # Express server application
│   ├── index.html          # Frontend UI
│   ├── package.json        # Node.js dependencies
│   └── images/             # Profile images
└── docker-compose.yaml     # Multi-container configuration
```

## Features

- View user profile information
- Update user profile (name, email, interests)
- Profile picture display
- Data persistence with MongoDB
- Admin interface via Mongo Express

## Prerequisites

- Docker installed on your system
- Docker Compose installed

## Quick Start

### Using Docker Compose (Recommended)

1. **Clone the repository**
   ```bash
   git clone https://github.com/Syedshara/docker-learning.git
   cd docker-learning
   ```

2. **Build the application image**
   ```bash
   cd app
   docker build -t my-app:1.2 .
   cd ..
   ```

3. **Start all services**
   ```bash
   docker-compose up -d
   ```

4. **Access the application**
   - Application: http://localhost:3001
   - Mongo Express: http://localhost:8081

5. **Stop all services**
   ```bash
   docker-compose down
   ```

## Services Configuration

### Application Service (my-app)
- **Port:** 3001 → 3000
- **Image:** my-app:1.2
- **Function:** Main web application

### MongoDB Service
- **Port:** 27027 → 27017
- **Credentials:** admin/password
- **Volume:** mongo-data (persistent storage)
- **Function:** Database server

### Mongo Express Service
- **Port:** 8081
- **Function:** Web-based MongoDB administration
- **Connected to:** mongodb service

## Environment Variables

### Application (Dockerfile)
```
MONGO_DB_USERNAME=admin
MONGO_DB_PWD=password
```

### MongoDB
```
MONGO_INITDB_ROOT_USERNAME=admin
MONGO_INITDB_ROOT_PASSWORD=password
```

### Mongo Express
```
ME_CONFIG_MONGODB_ADMINUSERNAME=admin
ME_CONFIG_MONGODB_ADMINPASSWORD=password
ME_CONFIG_MONGODB_SERVER=mongodb
```

## API Endpoints

- `GET /` - Serve the main HTML page
- `GET /profile-picture` - Fetch user profile picture
- `GET /get-profile` - Retrieve user profile data
- `POST /update-profile` - Update user profile information

## Docker Commands Reference

### Building the Image
```bash
docker build -t my-app:1.2 ./app
```

### Running Containers
```bash
# Start all services
docker-compose up -d

# View running containers
docker ps

# View logs
docker-compose logs -f

# Stop all services
docker-compose down

# Remove volumes
docker-compose down -v
```

## Development Notes

- The application listens on port 3000 inside the container
- MongoDB connection uses `mongoUrlDocker` for container networking
- Data persists in the `mongo-data` volume
- The database name is `my-db`
- User profile is stored with `userid: 1`

## Troubleshooting

### Port Already in Use
If ports are occupied, modify the port mappings in `docker-compose.yaml`

### MongoDB Connection Issues
Ensure the MongoDB service is running:
```bash
docker-compose ps
```

### Container Logs
Check logs for debugging:
```bash
docker-compose logs mongodb
docker-compose logs my-app
```

## Learning Resources

This project demonstrates:
- Docker containerization concepts
- Multi-container applications with Docker Compose
- Container networking and service discovery
- Volume management for data persistence
- Environment variable configuration

## Author

Nana Janashia (Original Author)

## License

ISC
