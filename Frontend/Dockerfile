FROM node:16.14.0 AS builder

WORKDIR /app

COPY ./package.json /app/package.json
COPY ./package-lock.json /app/package-lock.json

RUN npm install

COPY . /app/

RUN node_modules/ ./bin/ng build

FROM nginx:latest

COPY --from=builder /app/dist /app