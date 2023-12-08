# FROM openjdk:11
# ARG JAR_FILE=target/*.jar
# COPY ${JAR_FILE} user-service.jar
# ENTRYPOINT ["java","-jar","/user-service.jar"]
# EXPOSE 9002

# Stage 1: Build Stage
FROM maven:3.8.3-openjdk-11 AS build
WORKDIR /app
COPY . /app
RUN mvn -f /app/pom.xml clean package

# Stage 2: Runtime Stage
FROM adoptopenjdk:11-jre-hotspot-alpine
WORKDIR /app
COPY --from=build /app/target/*.jar /app/user-service.jar
ENTRYPOINT ["java", "-jar", "/app/user-service.jar"]
EXPOSE 9002

