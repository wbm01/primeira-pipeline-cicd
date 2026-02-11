FROM golang:1.22.0-alpine3.19 as builder

WORKDIR /build

COPY go.mod go.sum ./
RUN go mod download

COPY . .

RUN CGO_ENABLED=0 GOOS=linux GOARCH=$TARGETARCH go build -o app .

FROM alpine:3.19

RUN adduser -D -u 1000 appuser
USER appuser

WORKDIR /app
COPY --from=builder --chown=appuser:appuser /build/app .

EXPOSE 5000
CMD ["./app"]