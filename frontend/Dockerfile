FROM registry.access.redhat.com/ubi9/nodejs-20:latest AS build

USER 0
WORKDIR /app

COPY package.json package-lock.json ./
RUN npm ci

COPY tsconfig.json webpack.config.js ./
COPY src/ src/
RUN npm run build

FROM registry.access.redhat.com/ubi9/nginx-124:latest

COPY --from=build /app/dist /opt/app-root/src
COPY nginx.conf /etc/nginx/nginx.conf

EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]
