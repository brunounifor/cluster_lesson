# Use an official Node.js runtime as a parent image
FROM node:16-alpine3.14

# Set the working directory to /app
WORKDIR /app

# Copy the application code to the container
COPY . /app

# Install any necessary dependencies
RUN yarn install

# Compile TypeScript code into JavaScript
RUN yarn build

# Define the command to start the app
CMD [ "yarn", "start"]