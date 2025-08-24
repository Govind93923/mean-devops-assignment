# --- Stage 1: Build the Angular application ---
FROM node:18-alpine AS build

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

# This command builds the app into the /app/dist/angular-15-crud folder
RUN npm run build -- --configuration production

# --- Stage 2: Serve the application using Nginx ---
FROM nginx:stable-alpine

# Copy the built static files from the 'build' stage
COPY --from=build /app/dist/angular-15-crud /usr/share/nginx/html

# ADD THIS LINE: Copy your new Nginx configuration into the container
COPY ./nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80