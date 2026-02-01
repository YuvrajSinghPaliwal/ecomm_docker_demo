# 🛒 Ecomm Docker Demo

Spring Boot application running with MySQL using Docker & Docker Compose.

---

## 🧰 Tech Stack

- Java 21
- Spring Boot
- Maven (Wrapper)
- Docker
- Docker Compose
- MySQL 8

---

## ✅ Prerequisites

Install:
- Docker Desktop
- Git
- Java 21+

Verify:
```bash
docker --version
java --version
git --version

🗂️ Project Structure

.
├── Dockerfile
├── docker-compose.yml
├── pom.xml
├── mvnw / mvnw.cmd
└── src/

🐳 Docker Setup (How it works)
1) Dockerfile (App Image)
   -> This builds a runnable container image for your Spring Boot app.
   -> Uses Java 21 runtime
   -> Copies the packaged JAR into the image
   -> Starts the application by running the JAR

2) docker-compose.yml (App + DB)
   -> This boots the full stack with one command.
   -> App and MySQL run on the same Docker network
   -> App reaches MySQL using the service name: mysql
   -> MySQL port is not exposed to the host (only internal access)
   -> Database data persists via a Docker volume
   -> Only port 8080 is exposed for the app

▶️ Run It (Step-by-step)
Step 1 — Build the JAR (local)
   -> mvnw.cmd clean package -DskipTests
   Output: target/demo-0.0.1-SNAPSHOT.jar

Step 2 — Build the Docker image
   -> docker build -t ecomm:1.0.0 .

Step 3 — Start the full stack (app + mysql)
   -> docker compose up -d

Step 4 — Watch logs (sanity check)
   MySQL logs:
      -> docker compose logs -f mysql
   App logs:
      -> docker compose logs -f app

Expected:
   MySQL → ready for connections
   App → Tomcat started on port 8080

🌐 Open the App
http://localhost:8080

🧹 Stop & Cleanup
Stop containers:
   -> docker compose down

Stop + remove DB data (fresh start):
   -> docker compose down -v

🏭 Production Notes (Keep in mind)
   -> Don’t use localhost inside containers
   -> Prefer environment variables for configuration
   ->Keep DB persistent with volumes
   ->Let Docker networking handle service discovery (use service names)


