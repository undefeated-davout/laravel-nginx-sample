# npmビルド用
FROM node:20.0.0 as node-build
COPY ./src /application
WORKDIR /application
RUN apt-get update \
  && npm i \
  && npm run build


# 実行環境
FROM nginx:1.23.4
WORKDIR /application
RUN apt-get update
COPY ./docker/nginx/ecs/conf.d/default.conf /etc/nginx/conf.d/default.conf
COPY --from=node-build /application/public /application/public/
EXPOSE 80
