FROM gradle:jdk11 AS builder

WORKDIR /home/gradle

COPY . .

RUN gradle wrapper

RUN ./gradlew build --no-daemon

FROM registry.access.redhat.com/ubi8/ubi

RUN dnf install -y java-11-openjdk.x86_64

COPY --from=builder /home/gradle/build/libs/*.jar ./app.jar

EXPOSE 8080/tcp

CMD ["java", "-jar", "./app.jar"]
