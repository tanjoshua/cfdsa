FROM golang:1.22.3-alpine3.20 AS builder

WORKDIR /app

COPY go.mod .
COPY go.sum .
COPY main.go .

RUN go build -o main main.go

FROM alpine:3.20

WORKDIR /app

COPY --from=builder /app/main main
COPY public public
COPY templates templates


RUN apk update && apk add curl

ENV PORT=3000

EXPOSE ${PORT}

HEALTHCHECK --interval=30s --timeout=30s --start-period=5s --retries=3 \
    CMD curl -s http://localhost:${PORT}/healthz || exit 1


ENTRYPOINT /app/main