# Gradle Java App with Docker and Jenkins

A simple Java app built with Gradle, containerized using Docker, and deployed using Jenkins CI/CD.

## Run Locally

```bash
./gradlew build
java -jar build/libs/*.jar
```

## Docker Build

```bash
docker build -t gradle-java-app .
docker run -p 8080:8080 gradle-java-app
```
