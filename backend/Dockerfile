FROM golang:1.21-alpine AS builder

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

WORKDIR /app/cmd/app
COPY . .
RUN go build -o main .

FROM alpine:latest

RUN addgroup -S app && adduser -S app -G app

WORKDIR /app

COPY --from=builder --chown=app:app /app/cmd/app/main .

USER app

EXPOSE 8081

CMD ["./main"]