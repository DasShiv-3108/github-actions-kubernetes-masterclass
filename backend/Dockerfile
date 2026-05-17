# Stage 1: Build
FROM golang:1.24-alpine AS builder

WORKDIR /app

COPY go.mod go.sum ./

# Auto fix dependencies
RUN go mod tidy && go mod download

COPY . .

RUN CGO_ENABLED=0 go build -ldflags="-s -w" -o skillpulse .

# Stage 2: Run
FROM alpine:3.23

RUN apk --no-cache add ca-certificates

WORKDIR /app

COPY --from=builder /app/skillpulse .

EXPOSE 8080

CMD ["./skillpulse"]