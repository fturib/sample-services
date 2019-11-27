
#build stage
FROM golang:alpine AS builder
WORKDIR /go/src/pet
COPY . .
RUN apk add --no-cache git
RUN go get -d -v ./...
RUN go install -v ./...
RUN ls -a /go/bin/pet

#final stage
FROM alpine:latest
RUN apk --no-cache add ca-certificates
COPY --from=builder /go/bin/pet /pet
ENTRYPOINT ./pet
LABEL Name=go-pet Version=0.0.1
EXPOSE 8080
