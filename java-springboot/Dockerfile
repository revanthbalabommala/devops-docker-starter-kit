FROM eclipse-temurin:21-jdk

WORKDIR /app

COPY /build/libs/poc-0.0.1-SNAPSHOT.jar app.jar

RUN echo "image copied into WORKDIR"

ENV APP_NAME=POC

EXPOSE 8080

ENTRYPOINT ["java","-jar", "app.jar"]