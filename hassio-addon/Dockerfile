ARG BUILD_FROM
ARG BUILD_ARCH

FROM $BUILD_FROM

ENV FRP_VERSION 0.51.1
ENV FRP_ARCH "arm64"
ENV LANG C.UTF-8


WORKDIR /app
COPY run.sh .

#update and install deps
RUN apk update && apk add --no-cache openssl wget

#download frp
RUN wget https://github.com/fatedier/frp/releases/download/v${FRP_VERSION}/frp_${FRP_VERSION}_linux_${FRP_ARCH}.tar.gz

#extract frpc-binary
RUN tar -zxf frp_${FRP_VERSION}_linux_${FRP_ARCH}.tar.gz frp_${FRP_VERSION}_linux_${FRP_ARCH}/frpc

#make symlink and delete archive
RUN rm *.tar.gz && ln -s $(ls frp_*/* -r) frpc
CMD [ "./run.sh" ]