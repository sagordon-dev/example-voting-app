# Base image
FROM python:3.13.0a3-bookworm

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Launch the app when the container runs
CMD ["gunicorn", "--bind", "0.0.0.0:80", "app:app"]