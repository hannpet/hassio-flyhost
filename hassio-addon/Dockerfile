ARG BUILD_FROM
ARG BUILD_ARCH

FROM $BUILD_FROM

ENV FRP_VERSION 0.51.1
ENV LANG C.UTF-8


WORKDIR /app
COPY run.sh .

#frp has other arch-endings
RUN if [[ ${BUILD_ARCH} = aarch ]] ; then ARCH=arm64
RUN if [[ ${BUILD_ARCH} = amd64 ]] ; then ARCH=amd64

#update and install deps
RUN apk update && apk add --no-cache openssl wget

#download frp
RUN wget https://github.com/fatedier/frp/releases/download/v${FRP_VERSION}/frp_${FRP_VERSION}_linux_${ARCH}.tar.gz

#extract frpc-binary
RUN tar -zxf frp_${FRP_VERSION}_linux_${ARCH}.tar.gz frp_${FRP_VERSION}_linux_${ARCH}/frpc

#make symlink and delete archive
RUN rm *.tar.gz && ln -s $(ls frp_*/* -r) frpc
CMD [ "./run.sh" ]