FROM node:18-alpine AS builder

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

ENV NODE_OPTIONS=--openssl-legacy-provider
RUN npm run build

FROM node:18-alpine

RUN npm install -g serve

WORKDIR /usr/src/app

COPY --from=builder /app/dist ./dist

EXPOSE 80

CMD ["serve", "-s", "dist", "-l", "80"]