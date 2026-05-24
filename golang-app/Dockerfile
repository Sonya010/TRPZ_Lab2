FROM golang:1.22 AS builder

WORKDIR /app
COPY . .

RUN go mod download
RUN CGO_ENABLED=0 GOOS=linux go build -o server ./main.go

FROM gcr.io/distroless/static-debian12

COPY --from=builder /app/server /server
COPY --from=builder /app/templates /templates

EXPOSE 8080

CMD ["/server", "serve"]