####### Build the jar with maven #######
FROM maven:3.8.3-openjdk-17 AS builder

WORKDIR /app

COPY pom.xml .

RUN mvn dependency:go-offline -B

COPY src ./src

RUN mvn package

FROM openjdk:17-oracle AS binary



COPY --from=builder /app/target/xpenz-1.0.0-SNAPSHOT.jar /usr/local/bin


WORKDIR /tmp
USER ${user}

EXPOSE 8080

FROM binary AS debugable
CMD [ "/usr/local/openjdk-17/bin/java","-jar","-agentlib:jdwp=transport=dt_socket,server=y,address=8777,suspend=n", "/usr/local/bin/xpenz-1.0.0-SNAPSHOT.jar" ]


FROM binary AS runable

CMD [ "/usr/local/openjdk-17/bin/java", "-jar", "/usr/local/bin/xpenz-1.0.0-SNAPSHOT.jar" ]