FROM node:16-slim AS build

WORKDIR /build
COPY . .
RUN npm ci
RUN npm run build

FROM nginx:latest
RUN apt-get update -y \
    && apt-get install -yq \
    apache2-utils
RUN mkdir -p /etc/apache2 && htpasswd -cbm /etc/apache2/.htpasswd quramy hogehoge
COPY ./docker/nginx/nginx.conf /etc/nginx/nginx.conf
COPY --from=build /build/dist/ /var/www/html/
