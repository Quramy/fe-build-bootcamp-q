FROM node:16-slim AS build

WORKDIR /build
COPY . .
RUN npm ci
RUN npm run build

FROM nginx:latest
COPY ./docker/nginx/nginx.conf /etc/nginx/nginx.conf
COPY --from=build /build/dist/ /var/www/html/
