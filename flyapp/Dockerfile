FROM alpine:latest

ENV VERSION 0.51.2

WORKDIR /app
COPY frps.ini .
RUN wget https://github.com/fatedier/frp/releases/download/v${VERSION}/frp_${VERSION}_linux_amd64.tar.gz && \
    tar -xf frp_${VERSION}_linux_amd64.tar.gz --strip-components 1 frp_${VERSION}_linux_amd64/frps && \
    rm frp_${VERSION}_linux_amd64.tar.gz

ENTRYPOINT ["/app/frps"]
CMD ["-c","/app/frps.ini"]