# Stage de build optimisé
FROM maven:3.8.4-openjdk-17-slim AS build
WORKDIR /app
COPY pom.xml .
COPY api-gateway/pom.xml api-gateway/
RUN mvn dependency:go-offline -pl api-gateway || true
COPY . .
RUN mvn package -DskipTests -pl api-gateway -am -T 2C

# Stage final (runtime)
FROM eclipse-temurin:17-jre-alpine
RUN apk add --no-cache curl
WORKDIR /app
COPY --from=build /app/api-gateway/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-XX:+UseContainerSupport", "-XX:MaxRAMPercentage=75.0", "-jar", "/app/app.jar"]