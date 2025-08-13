# Use an official Node.js runtime as a parent image
FROM node:20-alpine

# Set the working directory in the container
WORKDIR /app/apps/api

# Copy package.json and pnpm-lock.yaml (or yarn.lock/package-lock.json)
# to leverage Docker cache for dependencies
COPY package.json pnpm-lock.yaml ./

# Install dependencies
RUN pnpm install --prod

# Copy the rest of the application code
COPY . .

# Build the TypeScript application (if applicable)
# RUN pnpm build

# Expose the port your API listens on
EXPOSE 3001

# Define the command to run your API
CMD ["pnpm", "run", "dev"]