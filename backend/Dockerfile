# Stage 1: Build Spring Boot app
FROM maven:3.9.4-eclipse-temurin-17 AS build

WORKDIR /app

COPY pom.xml .

RUN mvn dependency:go-offline -B

COPY src ./src

RUN mvn clean package -DskipTests

# Use an official OpenJDK image as a parent image
FROM openjdk:17-jdk-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy the built jar file into the container
COPY target/*.jar app.jar

# Expose the port your Spring Boot app runs on
EXPOSE 8080

# Run the jar file
ENTRYPOINT ["java", "-jar", "app.jar"]
