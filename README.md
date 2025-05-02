# MERN-DOCKER-APP

A fully containerized MERN (MongoDB, Express.js, React, Node.js) stack application built with Docker and orchestrated with Docker Compose.



## 🚀 Features

- **React Frontend**: Modern, responsive user interface
- **Express.js Backend**: RESTful API endpoints
- **MongoDB Database**: NoSQL database for data persistence
- **Docker Containers**: Isolated environments for each component
- **Docker Compose**: Single-command orchestration of the entire application stack

## 📋 Prerequisites

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## 🛠️ Quick Start

1. Clone this repository:
   ```bash
   git clone https://github.com/sivaprasad2646/Mern-Docker-App
   cd MERN-DOCKER-APP
   ```

2. Launch the application stack:
   ```bash
   docker-compose up
   ```

3. Access the application:
   - Frontend: http://localhost:3000
   - Backend API: http://localhost:5000
   - MongoDB: mongodb://localhost:27017

## 🏗️ Project Structure

```
mern-docker-feedback-app/
├── docker-compose.yml        # Main configuration for all services
├── backend/                  # Express.js server
│   ├── Dockerfile            # Backend container configuration
│   ├── package.json          # Node.js dependencies
│   ├── server.js             # Main server file
│   └── ...
├── frontend/                 # React application
│   ├── Dockerfile            # Frontend container configuration
│   ├── package.json          # React dependencies
│   ├── src/                  # React source code
│   └── ...
└── docs/                     # Documentation assets
    └── architecture-diagram.png
```

## 🐳 Docker Compose Configuration

The `docker-compose.yml` file orchestrates the entire application stack:

```yaml
version: '3'

services:
  # MongoDB Database
  mongodb:
    image: mongo:latest
    container_name: mongodb
    restart: always
    ports:
      - "27017:27017"
    volumes:
      - mongodb_data:/data/db
    networks:
      - mern-network

  # Backend API
  backend:
    build: ./backend
    container_name: mern-backend
    restart: always
    ports:
      - "5000:5000"
    environment:
      - MONGODB_URI=mongodb://mongodb:27017/feedback-app
      - PORT=5000
    depends_on:
      - mongodb
    networks:
      - mern-network

  # Frontend Application
  frontend:
    build: ./frontend
    container_name: mern-frontend
    restart: always
    ports:
      - "3000:3000"
    depends_on:
      - backend
    networks:
      - mern-network

networks:
  mern-network:
    driver: bridge

volumes:
  mongodb_data:
```

## 📝 API Endpoints

The application includes a RESTful API for handling data. Below are the available endpoints:

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET    | /api/data | Get all data entries |
| POST   | /api/data | Create new data entry |
| GET    | /api/data/:id | Get specific data by ID |
| PUT    | /api/data/:id | Update specific data |
| DELETE | /api/data/:id | Delete specific data |

*Note: Modify the endpoints according to your specific implementation.*

## 🧪 Development

To run individual services for development:

### Frontend Only

```bash
cd frontend
npm install
npm start
```

### Backend Only

```bash
cd backend
npm install
npm run dev
```

## 🔧 Environment Variables

Create `.env` files in both frontend and backend directories for local development, or specify them in the docker-compose.yml for containerized deployment.

## 📚 Lessons Learned

This project demonstrates the power of Docker Compose for orchestrating multi-container applications. Key benefits include:

- **Simplified Configuration**: Define all services in a single YAML file
- **Service Isolation**: Each component runs in its own container
- **Environment Consistency**: Same setup works across development and production
- **Simple Deployment**: One command to build and run the entire stack
- **Network Management**: Automatic service discovery and communication

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 📧 Contact

Your Name - sivaprasad

Project Link: https://github.com/sivaprasad2646/Mern-Docker-App

---

⭐ Don't forget to star this repository if you found it useful! ⭐
