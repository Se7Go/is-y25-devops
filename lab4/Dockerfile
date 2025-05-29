FROM alpine:latest AS builder

RUN apk add --no-cache openjdk17 maven

ENV APP_HOME=/app

WORKDIR $APP_HOME

COPY pom.xml .
COPY src ./src

RUN mvn clean package -DskipTests

FROM alpine:latest as run

RUN apk add --no-cache openjdk17

ENV APP_HOME=/app

WORKDIR $APP_HOME

COPY --from=builder $APP_HOME/target/*.jar app.jar

ENV JAVA_HOME=/usr/lib/jvm/java-17-openjdk \
    PATH="$PATH:/usr/lib/jvm/java-17-openjdk/bin"

ENTRYPOINT ["java", "-jar", "app.jar"]