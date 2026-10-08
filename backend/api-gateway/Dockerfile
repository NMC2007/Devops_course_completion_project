FROM gradle:8-jdk17 AS builder
WORKDIR /app

COPY api-gateway ./api-gateway
RUN cd api-gateway && gradle build -x test

# Stage 2: Run the application
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
COPY --from=builder /app/api-gateway/build/libs/*.jar app.jar
EXPOSE 8686
ENTRYPOINT ["java", "-jar", "app.jar"]
