FROM node:18-alpine AS build-stage

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

RUN npm install -g @angular/cli && ng build --configuration production

FROM nginx:stable-alpine-slim

COPY nginx.conf /etc/nginx/conf.d/default.conf

COPY --from=build-stage /app/dist/my-angular-app/browser /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]