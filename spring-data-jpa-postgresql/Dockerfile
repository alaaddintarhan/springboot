# https://stackoverflow.com/questions/27767264/how-to-dockerize-maven-project-and-how-many-ways-to-accomplish-it
#
# Build stage
#
FROM maven:3.6.0-jdk-11-slim AS build
COPY src /home/app/src
COPY pom.xml /home/app
RUN mvn -f /home/app/pom.xml clean package

#
# Package stage
#
# For Java 8, try this
# FROM openjdk:8-jdk-alpine
# For Java 11, try this
FROM adoptopenjdk/openjdk11:alpine-jre
# Refer to Maven build -> finalName
ARG JAR_FILE=target/spring-boot-data-jpa-1.0.jar
# Refer to Maven build -> finalName
COPY --from=build /home/app/${JAR_FILE} ${JAR_FILE}
# cd /opt/app
WORKDIR /opt/app
# cp target/spring-boot-web.jar /opt/app/app.jar
COPY ${JAR_FILE} app.jar
# java -jar /opt/app/app.jar
ENTRYPOINT ["java","-jar","app.jar"]

## sudo docker run -p 8080:8080 -t spring-boot-data-jpa:1.0
## sudo docker run -p 80:8080 -t spring-boot-data-jpa:1.0
## sudo docker run -p 443:8443 -t spring-boot-data-jpa:1.0