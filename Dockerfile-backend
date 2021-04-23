FROM openjdk:11-jdk
ADD target/springboot-0.0.1-SNAPSHOT.jar /code/app.jar
WORKDIR /code/
EXPOSE 8080
ENV MYSQL_DATABASE=""
CMD ["java", "-jar", "/code/app.jar"]
