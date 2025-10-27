# Stage 1: Build Stage (for installing dependencies)
FROM node:20-alpine AS builder

WORKDIR /app

# Copy package.json and package-lock.json to leverage Docker layer caching
COPY package*.json ./

# Install dependencies
RUN npm install --omit=dev

# Copy the rest of the application code
COPY . .

# If you have a build step (e.g., for TypeScript), uncomment and adjust this line
# RUN npm run build

# Stage 2: Production Stage (for a smaller final image)
FROM node:20-alpine

WORKDIR /app

# Copy only the necessary files from the builder stage
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app .

# Expose the port your Express app listens on
EXPOSE 3000

# Command to run your application
CMD ["node", "server.js"]