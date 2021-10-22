FROM diamol/golang as builder

COPY main.go .

RUN go build -o /server


FROM diamol/base

ENV USER=sixeyed

CMD ["/web/server"]

EXPOSE 80

WORKDIR /web
COPY --from=builder /server .

RUN chmod +x server

COPY index.html .




