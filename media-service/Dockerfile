# Stage de build optimisé
FROM maven:3.8.4-openjdk-17-slim AS build
WORKDIR /app
COPY pom.xml .
COPY media-service/pom.xml media-service/
RUN mvn dependency:go-offline -pl media-service || true
COPY . .
RUN mvn package -DskipTests -pl media-service -am -T 2C

# Stage final (runtime)
FROM eclipse-temurin:17-jre-alpine
RUN apk add --no-cache curl
WORKDIR /app
COPY --from=build /app/media-service/target/*.jar app.jar
EXPOSE 8083
ENTRYPOINT ["java", "-XX:+UseContainerSupport", "-XX:MaxRAMPercentage=75.0", "-jar", "/app/app.jar"]