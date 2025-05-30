# # Step 1: Build the React app
# FROM node:22-alpine AS build

# WORKDIR /app

# # Install dependencies
# COPY package.json package-lock.json ./
# RUN npm install

# # Copy all source code
# COPY . .

# # Set the API base URL for the React build
# ENV REACT_APP_API_BASE=https://django.pumej.com/api

# # Build the React app
# RUN npm run build

# # Step 2: Serve the app with Nginx
# FROM nginx:alpine

# # Remove default nginx static content
# RUN rm -rf /usr/share/nginx/html/*

# # Copy the built React files from build stage
# COPY --from=build /app/build /usr/share/nginx/html

# # Replace the default nginx config with custom config
# COPY nginx.conf /etc/nginx/conf.d/default.conf

# # Expose port 80 (default for nginx)
# EXPOSE 80

# # Run nginx in the foreground
# CMD ["nginx", "-g", "daemon off;"]

# Step 1: Build the React app
FROM node:22-alpine AS build

WORKDIR /app

# Install dependencies
COPY package.json package-lock.json ./
RUN npm install

# Copy all source code
COPY . .

# Set the API base URL for the React build
ENV REACT_APP_API_BASE=https://django.pumej.com/api

# Build the React app
RUN npm run build

# Step 2: Serve the app with Nginx
FROM nginx:alpine

RUN rm -rf /usr/share/nginx/html/*
COPY --from=build /app/build /usr/share/nginx/html

# Replace the default nginx config with custom config
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 3001

CMD ["nginx", "-g", "daemon off;"]