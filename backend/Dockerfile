# Use an official Node.js runtime as a parent image
FROM node:16-alpine3.14

# Set the working directory to /app
WORKDIR /app

# Copy the application code to the container
COPY . /app

# Install any necessary dependencies
RUN npm install

# Build dispensable because application is pure JavaScript

# Define the command to start the app
CMD [ "npm", "run", "start"]