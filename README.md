In this DevOps task, you need to build and deploy a full-stack CRUD application using the MEAN stack (MongoDB, Express, Angular 15, and Node.js). The backend will be developed with Node.js and Express to provide REST APIs, connecting to a MongoDB database. The frontend will be an Angular application utilizing HTTPClient for communication.  

The application will manage a collection of tutorials, where each tutorial includes an ID, title, description, and published status. Users will be able to create, retrieve, update, and delete tutorials. Additionally, a search box will allow users to find tutorials by title.

## Project setup

### Node.js Server

cd backend

npm install

You can update the MongoDB credentials by modifying the `db.config.js` file located in `app/config/`.

Run `node server.js`

### Angular Client

cd frontend

npm install

Run `ng serve --port 8081`

You can modify the `src/app/services/tutorial.service.ts` file to adjust how the frontend interacts with the backend.

Navigate to `http://localhost:8081/`
Deployment Documentation: MEAN Stack Tutorial Management System
This document outlines the end-to-end process of taking a MEAN stack application from a local development state to a fully automated, containerized cloud environment. The project manages a tutorial database, allowing for full CRUD operations through a modern web interface.

Project Concept and Logic
The application is structured as a distributed system where each layer handles a specific responsibility. By separating these concerns, the application becomes easier to maintain and scale.

User Interface: Built with Angular 15, providing a responsive experience for managing tutorial data. It communicates with the backend through standardized HTTP requests.

API Layer: A Node.js and Express server that acts as the bridge between the user and the data. It validates requests and manages the flow of information.

Data Persistence: A MongoDB instance stores tutorial records, including titles, descriptions, and publication status.

Containerization and Image Management
To solve the "it works on my machine" problem, the entire environment is defined as code using Docker. This ensures that the application runs identically on a local laptop as it does on a production server.

Optimized Builds: I used multi-stage Docker builds for the Angular frontend. This approach compiles the application in a temporary environment and only moves the final, lightweight production files to the server, significantly reducing the final image size.

Orchestration: Rather than managing containers individually, I utilized Docker Compose to define the relationship between the database, the API, and the UI. This allows the entire stack to be launched with a single command.

Registry: Images are hosted on Docker Hub, serving as a centralized source of truth for the deployment pipeline.

Cloud Infrastructure and Reverse Proxy
The application is hosted on an Ubuntu-based Virtual Machine. To make the services accessible and secure, I implemented a gateway strategy.

Nginx Integration: Instead of exposing multiple ports to the public, I configured Nginx as a reverse proxy on Port 80. It listens for incoming traffic and intelligently routes it to the correct container.

Networking: The internal communication between Node.js and MongoDB happens on a private Docker network, which keeps the database isolated from the public internet for better security.

Automation and CI/CD
To ensure that the application is always up to date, I built an automated pipeline that handles the deployment lifecycle. This removes the need for manual intervention and reduces the risk of human error during updates.

Continuous Integration: Whenever code is pushed to the repository, the pipeline automatically builds new Docker images to verify that the code compiles and the environment is stable.

Continuous Deployment: Once the build is successful, the pipeline securely connects to the Ubuntu VM via SSH, pulls the latest images from Docker Hub, and restarts the services. This ensures that the live application always reflects the most recent changes in the repository.

Verification and Deliverables
The following components are included in this repository to verify the successful implementation of the task:

Configuration Files: All Dockerfiles, the Docker Compose YAML, and the CI/CD workflow scripts.

Deployment Evidence: The repository contains a dedicated section for screenshots demonstrating the successful build process, the Docker Hub repository status, and the application running on the cloud VM.

Live Environment: The cloud server remains active, with all services managed by Docker and accessible via the VM’s public IP address.

final port number - http://51.20.121.209/
