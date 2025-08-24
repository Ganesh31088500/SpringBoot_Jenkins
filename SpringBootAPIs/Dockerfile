FROM eclipse-temurin:17-jdk-alpine as builder
WORKDIR /app
COPY pom.xml .
COPY mvnw .
COPY .mvn .mvn

RUN chmod +x mvnw 
RUN ./mvnw dependency:go-offline -B
COPY src src
RUN ./mvnw -B clean package -DskipTests

FROM eclipse-temurin:17-jre-alpine

RUN addgroup -S app && adduser -S app -G app
USER app
WORKDIR /app
COPY --from=builder /app/target/*.jar app.jar
EXPOSE 8080 
ENTRYPOINT [ "java","-jar","app.jar" ]
