# Use a specific version of the maven image for the build stage
FROM maven:3.6.3-jdk-11 AS maven_build

# Set the working directory in the build stage
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Run the maven build, skipping tests for the build stage
RUN mvn package -D skipTests

# Use a specific version of the openjdk image for the runtime stage
FROM openjdk:11-jre-alpine3.9

# Copy the jar file from the build stage to the runtime stage
COPY --from=maven_build /app/target/worker-jar-with-dependencies.jar /worker-jar-with-dependencies.jar

# Launch the application when the container starts
CMD ["java", "-jar", "/worker-jar-with-dependencies.jar"]