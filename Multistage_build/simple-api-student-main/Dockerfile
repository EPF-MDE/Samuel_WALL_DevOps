FROM eclipse-temurin:17-jdk-alpine
# Build Main.java with JDK
# TODO : in next steps (not now)

FROM eclipse-temurin:17-jre-alpine
# Copy resource from previous stage
COPY --from=0 /usr/src/Main.class .
# Run java code with the JRE
# TODO : in next steps (not now)

# Build
FROM maven:3.8.6-amazoncorretto-17 AS myapp-build
ENV MYAPP_HOME /opt/myapp
WORKDIR $MYAPP_HOME
COPY pom.xml .
COPY src ./src
RUN mvn package -DskipTests

# Run
FROM amazoncorretto:17
ENV MYAPP_HOME /opt/myapp
WORKDIR $MYAPP_HOME
COPY --from=myapp-build $MYAPP_HOME/target/*.jar $MYAPP_HOME/myapp.jar

ENTRYPOINT java -jar myapp.jar
