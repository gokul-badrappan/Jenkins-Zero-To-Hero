# Stage 1: Build the JAR using Maven + Java 17
FROM maven:3.9.4-eclipse-temurin-17 as builder

WORKDIR /app
COPY . .
RUN mvn clean package -DskipTests

# Stage 2: Lightweight runtime with Java 17
FROM eclipse-temurin:17-jdk-alpine

WORKDIR /opt/app

# Copy JAR from the builder stage
COPY --from=builder /app/target/*.jar app.jar

# Optional health check for k8s readiness probe
HEALTHCHECK --interval=30s --timeout=10s --start-period=10s --retries=3 \
  CMD wget --spider http://localhost:8080/actuator/health || exit 1

ENTRYPOINT ["java", "-jar", "app.jar"]
