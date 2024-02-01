# Use a specific version of the node image for reproducibility
FROM node:14-alpine

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json before other files
# Utilizes Docker cache to save re-installing dependencies if unchanged
COPY package*.json ./

# Install nodemon globally, set npm registry, install dependencies and clean cache
RUN npm install -g nodemon && \
    npm config set registry https://registry.npmjs.org/ && \
    npm install && \
    npm cache clean --force

# Copy the rest of the application code to the work directory
COPY . /app

# Set the environment variable to tell the application to listen on port 80
ENV PORT=80

# Expose port 80 for the application
EXPOSE 80

# Use a non-root user to run our application
USER node

# Command to run the application
CMD ["node", "server.js"]