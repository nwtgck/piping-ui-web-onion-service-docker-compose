# NOTE: Multi-stage Build

FROM node:12.18.0-alpine as build

ENV PIPING_UI_WEB_REVISION v0.5.0

RUN apk add --no-cache git
RUN echo -e "build_user\nbuild_user" | adduser build_user
USER build_user
WORKDIR /home/build_user
RUN git clone https://github.com/nwtgck/piping-ui-web.git
WORKDIR piping-ui-web
RUN git checkout $PIPING_UI_WEB_REVISION
RUN npm ci
RUN npm run build


FROM nginx:alpine

LABEL maintainer="Ryo Ota <nwtgck@gmail.com>"

# Copy artifacts
COPY --from=build /home/build_user/piping-ui-web/dist /var/www
COPY ./nginx.conf /etc/nginx/conf.d/default.conf
