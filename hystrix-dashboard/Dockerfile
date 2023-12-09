#Stage 1
FROM maven:3.8.3-openjdk-11 AS build
WORKDIR /app
COPY pom.xml .
RUN mvn dependency:go-offline
COPY . /app
RUN mvn -f /app/pom.xml clean package -Dmaven.test.skip=true

#Stage 2
FROM adoptopenjdk/openjdk11:jre-11.0.9_11-alpine
WORKDIR /app
COPY --from=build /app/target/*.jar /app/user-service.jar
ENTRYPOINT ["java", "-jar", "/app/user-service.jar"]
EXPOSE 9295
