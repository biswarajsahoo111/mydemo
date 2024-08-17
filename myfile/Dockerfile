# Stage 1: Build the application
FROM golang:1.16 AS builder

# Set the working directory
WORKDIR /app

# Copy the source code
COPY . .

# Build the application
RUN go build -o my-app

# Stage 2: Create the final image
FROM alpine:latest

# Set the working directory
WORKDIR /root/

# Copy the binary from the builder stage
COPY --from=builder /app/my-app .

# Expose the application port
EXPOSE 8080

# Command to run the application
CMD ["./my-app"]

