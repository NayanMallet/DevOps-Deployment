FROM node:18-alpine AS build-front

WORKDIR /app
COPY package*.json ./
RUN npm install

COPY . .

ARG VITE_API_URL
ENV VITE_API_URL=${VITE_API_URL}

RUN npm run build

FROM nginx:stable AS prod-front
COPY --from=build-front /app/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
