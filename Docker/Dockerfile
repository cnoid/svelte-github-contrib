# Use the latest LTS version of Node.js
FROM node:lts

# Set the working directory in the Docker container
WORKDIR /usr/src/app

# Install pnpm
RUN npm install -g pnpm

# Copy package.json and other necessary files for dependency installation
COPY package.json ./
COPY pnpm-lock.yaml* ./

# Install dependencies
RUN pnpm i

# Copy the rest of your application's code
COPY . .

# Expose the port the app runs on
EXPOSE 5173

# Start the application
CMD ["pnpm", "run", "dev", "--host"]
