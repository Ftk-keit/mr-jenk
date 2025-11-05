# Stage de build optimisé
FROM maven:3.8.4-openjdk-17-slim AS build
WORKDIR /app
COPY pom.xml .
COPY eureka-server/pom.xml eureka-server/
RUN mvn dependency:go-offline -pl eureka-server || true
COPY . .
RUN mvn package -DskipTests -pl eureka-server -am -T 2C

# Stage final (runtime)
FROM eclipse-temurin:17-jre-alpine
RUN apk add --no-cache curl
WORKDIR /app
COPY --from=build /app/eureka-server/target/*.jar app.jar
EXPOSE 8761
ENTRYPOINT ["java", "-XX:+UseContainerSupport", "-XX:MaxRAMPercentage=75.0", "-jar", "/app/app.jar"]