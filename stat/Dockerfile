FROM golang:1.23 AS builder

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -o stat-app main.go

FROM alpine:latest
WORKDIR /app
COPY --from=builder /app/stat-app .

EXPOSE 8002
CMD ["./stat-app"]
