FROM maven:3.9.6-eclipse-temurin-17 AS build

WORKDIR /app

COPY pom.xml .

RUN mvn dependency:go-offline

COPY src ./src

RUN mvn clean package -DskipTests

RUN ls -la target

FROM openjdk:17-alpine

WORKDIR /app

COPY --from=build /app/target/*.jar /app/demo.jar

EXPOSE 9090

ENTRYPOINT ["java", "-jar", "demo.jar"]