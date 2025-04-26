
FROM maven:3.9-amazoncorretto-24-alpine AS builder

WORKDIR /app
COPY pom.xml .

# COPY src/main/resources/.env /app/.env
RUN mvn dependency:go-offline -B
COPY src ./src

RUN mvn clean package -DskipTests

FROM amazoncorretto:24

WORKDIR /app
COPY --from=builder /app/target/*.jar /app.jar

EXPOSE 4301
ENTRYPOINT ["java", "-jar", "/app.jar"]