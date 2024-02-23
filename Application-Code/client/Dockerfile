FROM node:20.11.1 20.8.0-alpine@sha256:37750e51d61bef92165b2e29a77da4277ba0777258446b7a9c99511f119db096 as base

FROM base as builder

WORKDIR /usr/src/app
COPY package*.json ./
RUN npm install --only=production

FROM base

WORKDIR /usr/src/app
COPY ./ ./client
RUN cd client && npm install && npm run build --prod
# Use official nginx image as the base image
FROM nginx:latest

# Copy the build output to replace the default nginx contents.
COPY --from=web-build /usr/src/app/client/dist/client/ /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose port 4200
EXPOSE 4200