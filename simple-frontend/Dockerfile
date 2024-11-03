#Stage 1 building
FROM maven:3.8.8-eclipse-temurin-11 AS builder

WORKDIR /app

COPY pom.xml ./
COPY src  ./src

RUN mvn clean package

#Stage 2 for running the jar/war created after building in above stage
FROM tomcat:9.0.75-jdk17

COPY --from=builder /app/target/my-webapp.war /usr/local/tomcat/webapps/

# Change the Tomcat port from 8080 to 8082 by modifying server.xml
RUN sed -i 's/port="8080"/port="8082"/g' /usr/local/tomcat/conf/server.xml

EXPOSE 8082

CMD ["catalina.sh","run"]
