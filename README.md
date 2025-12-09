💻 Project 2: Two-Tier Application Containerization
This project demonstrates the containerization and orchestration of a modern two-tier application, consisting of an Angular SSR Frontend and a PostgreSQL Database, integrating security scanning into the deployment workflow.

🛠️ Requirements & Key Technologies

Technology         Tier                     Component Purpose
Docker             Containerization         Packaging the application into portable images.
Docker Compose     Orchestration            Defining and running the multi-container application.
Docker Scout       Security Scanning        Analyzing built images for known vulnerabilities (CVEs).
Angular 19+ (SSR)  Client Tier              "The To-Do List user interface, served via Node.js/Express."
PostgreSQL 14      Data Tier                Persistent data storage for the to-do list items.

📂 Project Structure
.
├── to-do-list/              # Client Tier: Angular source, package.json, and Dockerfile
│   └── Dockerfile           # Multi-stage build for Node.js SSR runtime
├── database/                # Data Tier: Database setup files
│   └── init.sql             # SQL script to create the 'todos' table
└── docker-compose.yml       # Orchestrates and links both services


🚀 Usage Instructions
Prerequisites
Docker Engine and Docker Compose (V2+) installed.

Docker Hub Account (required for docker scout).

1. Build and Run the Application
Navigate to the project root directory and run this command. It builds the Angular image and launches both services in detached mode (-d).

Bash

docker compose up --build -d
2. Verify Container Status
Check that both the frontend (todo-angular-client) and the database (todo-db) containers are running successfully.

Bash

docker compose ps
3. Access the Application
The Angular SSR application is mapped from the internal container port 4000 to port 80 on your host machine.

URL: http://localhost


🔒 Security and Performance (Non-Functional Requirements)
Performance Optimization
Multi-Stage Build: Used in the Dockerfile to discard build dependencies and significantly reduce the final image size.

Alpine Base Images: Both services use minimal Alpine Linux base images for quicker container startup times and a smaller deployment footprint.

Security Implementation
Image Scanning: The final project step involves integrating vulnerability scanning to ensure security standards are met before deployment. You must be logged in to Docker Hub.

Bash

docker scout cves todo-angular-client:latest
Immutability: Data persistence is handled via a Docker Volume (db-data), ensuring the application and database containers are disposable and the data is separate and safe.

4. Cleanup
Stop and remove all running containers, associated networks, and the persistent database volume.

Bash

docker compose down -v
