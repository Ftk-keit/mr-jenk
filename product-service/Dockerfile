# Stage de build (seulement si JAR n'existe pas)
FROM maven:3.8.4-openjdk-17-slim AS build
WORKDIR /app
COPY pom.xml .
COPY product-service/pom.xml product-service/
# Télécharger les dépendances seulement
RUN mvn dependency:go-offline -pl product-service || true
COPY . .
RUN mvn package -DskipTests -pl product-service -am -T 2C

# Stage final (runtime)
FROM eclipse-temurin:17-jre-alpine
RUN apk add --no-cache curl
WORKDIR /app
# Copier depuis le build Maven local SI disponible, sinon depuis le stage build
COPY --from=build /app/product-service/target/*.jar app.jar
EXPOSE 8082
ENTRYPOINT ["java", "-XX:+UseContainerSupport", "-XX:MaxRAMPercentage=75.0", "-jar", "/app/app.jar"]