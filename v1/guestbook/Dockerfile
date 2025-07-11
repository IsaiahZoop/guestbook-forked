# Stage 1: Build the Go binary
FROM golang:1.18 AS builder

WORKDIR /app

COPY main.go .

RUN go mod init guestbook
RUN go mod tidy

RUN go build -o main main.go

# Stage 2: Create the final image
FROM ubuntu:18.04

# Copy the built Go binary from the builder stage
COPY --from=builder /app/main /app/guestbook

# Copy frontend assets
COPY public/index.html /app/public/index.html
COPY public/script.js /app/public/script.js
COPY public/style.css /app/public/style.css
COPY public/jquery.min.js /app/public/jquery.min.js

WORKDIR /app

# Expose the app port
EXPOSE 3000

# Run the app
 CMD ["./guestbook"]