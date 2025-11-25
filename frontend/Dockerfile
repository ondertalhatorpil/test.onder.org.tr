FROM node:20-alpine as build
WORKDIR /app

ARG REACT_APP_API_URL
ENV REACT_APP_API_URL=${REACT_APP_API_URL}

COPY package*.json ./

# ajv'yi manuel ekle ve tüm paketleri kur
RUN npm cache clean --force && \
    npm install --legacy-peer-deps && \
    npm install ajv@^8.12.0 --save-dev --legacy-peer-deps

COPY . .
RUN npm run build

FROM nginx:alpine
COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]