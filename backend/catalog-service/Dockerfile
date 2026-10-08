FROM gradle:8-jdk17 AS builder
WORKDIR /app

# Copy shared-auth-lib first and publish it to local maven repo
COPY shared-auth-lib ./shared-auth-lib
RUN cd shared-auth-lib && gradle publishToMavenLocal

# Copy service source and build
COPY catalog-service ./catalog-service
RUN cd catalog-service && gradle build -x test

# Stage 2: Run the application
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
COPY --from=builder /app/catalog-service/build/libs/*.jar app.jar
EXPOSE 8081
ENTRYPOINT ["java", "-jar", "app.jar"]
