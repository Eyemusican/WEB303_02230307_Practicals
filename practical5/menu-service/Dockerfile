FROM golang:1.23-alpine AS builder
WORKDIR /app
COPY go.mod ./
RUN go mod download
COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -o menu-service .

FROM alpine:latest
WORKDIR /root/
COPY --from=builder /app/menu-service .
EXPOSE 8082
CMD ["./menu-service"]