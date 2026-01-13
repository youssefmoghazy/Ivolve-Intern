FROM maven:3.9.6-eclipse-temurin-17

WORKDIR /app

COPY . .

# Build the jar
RUN mvn clean package -DskipTests

EXPOSE 8080

# Override Maven ENTRYPOINT
ENTRYPOINT ["java", "-jar", "target/demo-0.0.1-SNAPSHOT.jar"]

