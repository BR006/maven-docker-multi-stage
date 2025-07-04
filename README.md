# Docker Multi-Stage Build (Java Maven App)

This lab demonstrates how to use a multi-stage Docker build to compile and run a Java application using Maven.

---

## 🛠️ Technologies Used

- Java 17
- Maven
- Docker (Multi-Stage Build)

---

## 📁 Project Structure

```
.
├── Dockerfile
├── pom.xml
└── src/
```

---

## 🧱 Dockerfile Explanation

- **Stage 1:** Use Maven image to build the application.
- **Stage 2:** Use OpenJDK slim image to run the JAR only (lighter image).

```dockerfile
# Build Stage
FROM maven:3.8.5-openjdk-17 AS build
WORKDIR /app
COPY . .
RUN mvn clean package

# Run Stage
FROM openjdk:17-jdk-slim
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar
EXPOSE 8080
CMD ["java", "-jar", "app.jar"]
```

---

## 🚀 How to Run the Project

### 1️⃣ Build the Docker image

```bash
docker build -t java-multi-stage-app .
```

### 2️⃣ Run the container

```bash
docker run -d -p 8080:8080 --name java-app java-multi-stage-app
```

### 3️⃣ Test the app

Open your browser or use curl:

```bash
http://localhost:8080
```

### 4️⃣ Stop and remove the container

```bash
docker stop java-app
docker rm java-app
```

---

## 📦 Notes

- `target/` folder is ignored in version control (add it to `.gitignore`).
- Multi-stage builds help reduce image size by separating build and runtime environments.

---

## 💻 Author

Yousof Khaled 

