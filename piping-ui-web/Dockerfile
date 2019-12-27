# NOTE: Multi-stage Build

FROM node:12.14-alpine as build

ENV PIPING_UI_WEB_REVISION v0.4.20

RUN apk add --no-cache git
RUN echo -e "build_user\nbuild_user" | adduser build_user
USER build_user
WORKDIR /home/build_user
RUN git clone https://github.com/nwtgck/piping-ui-web.git
WORKDIR piping-ui-web
RUN git checkout $PIPING_UI_WEB_REVISION
RUN npm ci
RUN npm run build


# TODO: Use more proper image
# Python3
FROM python:3
LABEL maintainer="Ryo Ota <nwtgck@gmail.com>"

# Make directories
RUN mkdir -p /app
# Copy artifact
COPY --from=build /home/build_user/piping-ui-web/dist /app
WORKDIR /app

# Run entry (Run the server)
ENTRYPOINT ["python3", "-m", "http.server"]
