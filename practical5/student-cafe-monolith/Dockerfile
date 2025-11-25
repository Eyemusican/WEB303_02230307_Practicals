FROM golang:1.23-alpine AS builder
WORKDIR /app

# Copy only go.mod (not go.sum since it doesn't exist yet)
COPY go.mod ./

# Download dependencies (this will create go.sum automatically)
RUN go mod download

# Copy the rest of the code
COPY . .

# Build the application
RUN CGO_ENABLED=0 GOOS=linux go build -o menu-service .

FROM alpine:latest
WORKDIR /root/
COPY --from=builder /app/menu-service .
EXPOSE 8082
CMD ["./menu-service"]