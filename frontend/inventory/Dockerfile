# Use official Node.js image for build stage
FROM node:20-alpine AS build

WORKDIR /app

COPY inventory/package*.json ./
RUN npm install

COPY inventory/ ./
RUN npm run build -- --output-path=dist

# Use Nginx to serve the built Angular app
FROM nginx:alpine

# Remove default Nginx static assets
RUN rm -rf /usr/share/nginx/html/*

# Copy built Angular app from build stage
COPY --from=build /app/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
