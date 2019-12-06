FROM gradle:jdk11 AS builder

WORKDIR /home/gradle
COPY . .
RUN ./gradlew assemble

FROM registry.access.redhat.com/ubi8/ubi

RUN dnf install -y java-11-openjdk.x86_64

COPY --from=builder /home/gradle/build/libs/demo-0.0.1-SNAPSHOT.jar ./app.jar

EXPOSE 8080/tcp

CMD ["java", "-jar", "./app.jar"]
