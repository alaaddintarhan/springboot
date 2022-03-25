# https://stackoverflow.com/questions/27767264/how-to-dockerize-maven-project-and-how-many-ways-to-accomplish-it
#
# Build stage
#
FROM maven:3.6.0-jdk-11-slim AS build
COPY src /home/app/src
COPY pom.xml /home/app/pom.xml
RUN mvn -f /home/app/pom.xml clean package
RUN ls  /home/app/target

#
# Package stage
#
# For Java 8, try this FROM openjdk:8-jdk-alpine
# For Java 11, try this
FROM adoptopenjdk/openjdk11:alpine-jre as package
# Refer to Maven build -> finalName
ARG JAR_FILE=spring-boot-data-jpa-1.0.jar

# cd /opt/app
WORKDIR /opt/app

# cp spring-boot-data-jpa-1.0.jarfrom build to /opt/app/app.jar
COPY --from=build /home/app/target/${JAR_FILE}  app.jar

# java -jar /opt/app/app.jar
ENTRYPOINT ["java","-jar","app.jar"]

## sudo docker run -p 8080:8080 -t spring-boot-data-jpa:1.0
## sudo docker run -p 80:8080 -t spring-boot-data-jpa:1.0
## sudo docker run -p 443:8443 -t spring-boot-data-jpa:1.0