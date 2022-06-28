FROM golang:1.18.3-alpine3.15 as contract
WORKDIR /build
RUN apk update
RUN apk add --update --no-cache nodejs npm git make python3 gcc musl-dev linux-headers bash
RUN git submodule update
RUN npm i -g yarn
ADD ./genesis/package.json /build/package.json
RUN yarn || true
ADD ./genesis /build
RUN yarn compile

FROM golang:1.18.3-alpine3.15 as build
RUN apk update
RUN apk add --update --no-cache nodejs npm git make python3 gcc musl-dev linux-headers bash

WORKDIR /bas/
COPY --from=contract /build/build ./build
ADD ./nr-genesis/* .
RUN make build-create-genesis

FROM alpine:3.15

WORKDIR /opt/app/nr-create-genesis
RUN apk add --no-cache ca-certificates
COPY --from=build /bas/create-genesis ./
COPY --from=build /bas/nr-config.json ./
ENTRYPOINT ["./create-genesis"]
CMD ["nr-config.json"]