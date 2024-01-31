# Base Image: node:latest
FROM node:latest

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json before other files
# for better cache on Docker
COPY package*.json ./

# Build Instructions
RUN npm install -g nodemon && \
    npm config set registry https://registry.npm.taobao.org && \
    npm install && \
    npm ls && \
    npm cache clean --force

# Copy other source code to work directory
COPY . /app

# Ports to be exposed
EXPOSE 80

# Launch the app
CMD ["node", "server.js"]