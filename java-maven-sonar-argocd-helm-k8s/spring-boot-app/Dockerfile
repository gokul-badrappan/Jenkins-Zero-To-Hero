# Use Java 17 instead of Java 11
FROM eclipse-temurin:17-jdk-alpine

# Define the path to your built JAR file
ARG artifact=target/spring-boot-web.jar

# Set working directory inside the container
WORKDIR /opt/app

# Copy the built JAR file into the container
COPY ${artifact} app.jar

# Start the application
ENTRYPOINT ["java", "-jar", "app.jar"]
