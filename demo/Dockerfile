# Stage 1: Build the Maven project
FROM maven:3.8.4-openjdk-17 AS build

# Set the working directory in the container
WORKDIR /app

# Copy the pom.xml file and the source code to the container
COPY pom.xml .
COPY src ./src

# Build the Maven project
RUN mvn clean package

# Stage 2: Run the application
FROM openjdk:17-jdk-slim

# Set the working directory in the container
WORKDIR /app

# Copy the jar file from the previous stage
COPY --from=build /app/target/demo-0.0.1-SNAPSHOT.jar ./demo-0.0.1-SNAPSHOT.jar

# Expose port (if your application is a web application, specify the port here)
EXPOSE 8080

# Run the application
CMD ["java", "-jar", "demo-0.0.1-SNAPSHOT.jar", "--spring.config.location=file:/configs/demo/app.properties"]