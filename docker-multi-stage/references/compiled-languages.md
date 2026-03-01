# Multi-Stage: Compiled Languages (Go, Rust, Java)

## Go (Static Binary on Scratch)
Go can produce completely static binaries, allowing you to use `scratch` (the empty image) for the smallest possible runtime.

```dockerfile
FROM golang:1.22-alpine AS builder
WORKDIR /app
COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -ldflags="-s -w" -o /app/server

FROM scratch AS runtime
COPY --from=builder /app/server /server
COPY --from=builder /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/
USER 65534
ENTRYPOINT ["/server"]
```

## Rust (Static Linking with Musl)
Use the `musl` target to create a statically linked Rust binary that runs on `scratch`.

```dockerfile
FROM rust:1.75-alpine AS builder
RUN apk add --no-cache musl-dev
WORKDIR /app
COPY . .
RUN cargo build --release --target x86_64-unknown-linux-musl

FROM scratch AS runtime
COPY --from=builder /app/target/x86_64-unknown-linux-musl/release/app /app
USER 65534
ENTRYPOINT ["/app"]
```

## Java (JRE-only Runtime)
Use the full JDK only for building; switch to a lightweight JRE for the final image.

```dockerfile
FROM eclipse-temurin:21-jdk-alpine AS builder
WORKDIR /app
COPY . .
RUN ./gradlew build --no-daemon

FROM eclipse-temurin:21-jre-alpine AS runtime
WORKDIR /app
COPY --from=builder /app/build/libs/*.jar app.jar
USER nobody
ENTRYPOINT ["java", "-jar", "app.jar"]
```
