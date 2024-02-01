# Use a specific version of the maven image for the build stage
FROM maven:3.6.3-jdk-11 AS maven_build

# Set the working directory in the build stage
WORKDIR /app

# Copy the pom.xml file into the container at /app
COPY pom.xml /app

# Download the project dependencies
RUN mvn dependency:go-offline -B

# Copy the rest of the project files into the container at /app
COPY src /app/src

# Run the maven build, skipping tests for the build stage
RUN mvn package -D skipTests

# Use a specific version of the openjdk image for the runtime stage
FROM ibmjava:8-jre 

# Copy the jar file from the build stage to the runtime stage
COPY --from=maven_build /app/target/worker-jar-with-dependencies.jar /worker-jar-with-dependencies.jar

# Launch the application when the container starts
CMD ["java", "-jar", "/worker-jar-with-dependencies.jar"]