FROM golang:1.24 AS builder
RUN mkdir /app
WORKDIR /app
COPY go.* .
RUN go mod download
COPY . .
RUN CGO_ENABLED=0 go build -ldflags="-s -w" -o magpie ./cmd/magpie/...

FROM alpine
RUN apk add --no-cache tzdata
RUN mkdir /app /core
COPY --from=builder /app/magpie /app
CMD ["/app/magpie"]
