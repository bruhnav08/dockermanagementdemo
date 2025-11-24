# --- Stage 1: Build the React Application ---
FROM node:18-alpine AS build

WORKDIR /app

# Copy package definitions
COPY package*.json ./

# Install dependencies cleanly
RUN npm install

# Copy source code
COPY . .

# --- FIX: Fix permissions for executables ---
# This ensures that all binaries in node_modules/.bin are executable
RUN chmod +x node_modules/.bin/*

# Build the static files (creates /app/build)
RUN npm run build

# --- Stage 2: Serve with Nginx ---
FROM nginx:alpine

# Copy the build output from Stage 1 to Nginx's html folder
COPY --from=build /app/build /usr/share/nginx/html

# Remove default Nginx config
RUN rm /etc/nginx/conf.d/default.conf

# Copy our custom Nginx config
COPY nginx.conf /etc/nginx/conf.d/

# Expose HTTP port
EXPOSE 80

# Nginx starts automatically
