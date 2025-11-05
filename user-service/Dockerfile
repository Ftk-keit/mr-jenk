# Stage de build optimisé
FROM maven:3.8.4-openjdk-17-slim AS build
WORKDIR /app
COPY pom.xml .
COPY user-service/pom.xml user-service/
RUN mvn dependency:go-offline -pl user-service || true
COPY . .
RUN mvn package -DskipTests -pl user-service -am -T 2C

# Stage final (runtime)
FROM eclipse-temurin:17-jre-alpine
RUN apk add --no-cache curl
WORKDIR /app
COPY --from=build /app/user-service/target/*.jar app.jar
EXPOSE 8081
ENTRYPOINT ["java", "-XX:+UseContainerSupport", "-XX:MaxRAMPercentage=75.0", "-jar", "/app/app.jar"]