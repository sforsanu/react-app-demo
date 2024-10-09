FROM node:20-alpine AS builder

ENV NODE_ENV production
WORKDIR /app

COPY ./package*.json ./

RUN npm install --legacy-peer-deps --production=false
COPY . .
RUN npm run build

FROM nginx:alpine

COPY --from=builder /app/build /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80 443
CMD [ "nginx", "-g","daemon off;"]