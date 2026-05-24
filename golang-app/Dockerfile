FROM golang:1.22 AS builder

WORKDIR /app
COPY . .

RUN go mod download

RUN CGO_ENABLED=0 GOOS=linux go build -o server ./main.go

FROM scratch

COPY --from=builder /app/server /server

EXPOSE 8080

CMD ["/server", "serve"]