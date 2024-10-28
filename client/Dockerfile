# Stage 1: Build the React app
FROM node:22 AS build

# Set working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Set the VITE_SERVER_URL environment variable
ENV VITE_SERVER_URL="http://a53872b47837a45ecb4656ce30c3b821-2104944944.eu-west-1.elb.amazonaws.com:6001"

# Copy the rest of the application code
COPY . .

# Build the app
RUN npm run build

# Stage 2: Serve the React app using Nginx
FROM nginx:stable-alpine

# Copy the build output to the Nginx server root directory
COPY --from=build /app/dist /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start Nginx server
CMD ["nginx", "-g", "daemon off;"]
