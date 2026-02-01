Ecomm Docker Demo

Spring Boot application running with MySQL using Docker & Docker Compose.

Tech Stack

Java 21

Spring Boot

Maven (Wrapper)

Docker

Docker Compose

MySQL 8

Prerequisites

Make sure these are installed:

Docker Desktop

Git

Java 21+

Verify:

docker --version
java --version
git --version

Project Structure
.
├── Dockerfile
├── docker-compose.yml
├── pom.xml
├── mvnw / mvnw.cmd
└── src/

Docker Configuration
Dockerfile

What it does

Uses Java 21 runtime

Copies the packaged JAR

Runs the application

docker-compose.yml

Runs Spring Boot + MySQL together.

Key points

Containers communicate using service name mysql

MySQL port is not exposed to host

Database data is persisted using Docker volume

Only application port 8080 is exposed

Build & Run
1️⃣ Build Application
mvnw.cmd clean package -DskipTests


Creates:

target/demo-0.0.1-SNAPSHOT.jar

2️⃣ Build Docker Image
docker build -t ecomm:1.0.0 .

3️⃣ Start Application
docker compose up -d

4️⃣ Verify Logs
docker compose logs -f mysql
docker compose logs -f app


Expected:

MySQL → ready for connections

App → Tomcat started on port 8080

Access Application
http://localhost:8080

Stop & Cleanup
docker compose down


Remove database data:

docker compose down -v

Production Notes

No localhost usage inside containers

Externalized configuration via environment variables

Persistent database storage

Docker-network based service discovery
