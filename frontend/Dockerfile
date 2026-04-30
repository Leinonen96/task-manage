FROM node:22-alpine as build

WORKDIR /app

COPY package*.json ./
COPY frontend/package.json ./frontend/

RUN npm install --workspace=frontend --legacy-peer-deps

COPY frontend/ ./frontend/

WORKDIR /app/frontend

ARG VITE_API_URL
ENV VITE_API_URL=$VITE_API_URL

RUN npm run build

FROM nginx:alpine

COPY --from=build /app/frontend/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]