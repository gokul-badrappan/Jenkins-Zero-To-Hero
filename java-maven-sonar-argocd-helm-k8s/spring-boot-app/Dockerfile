# Stage 1: Build the JAR file (optional if you're building it in the pipeline)
FROM maven:3.9.4-eclipse-temurin-17 as build

WORKDIR /app
COPY . .
RUN mvn clean package -DskipTests

# Stage 2: Run the JAR file with Java 17
FROM eclipse-temurin:17-jdk-alpine

WORKDIR /opt/app

# Copy the JAR file from the build stage
COPY --from=build /app/target/spring-boot-web.jar app.jar

# Health check (optional)
HEALTHCHECK --interval=30s --timeout=10s --retries=3 CMD curl --fail http://localhost:8080/actuator/health || exit 1

ENTRYPOINT ["java", "-jar", "app.jar"]
