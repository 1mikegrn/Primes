FROM alpine:3.13 AS build

ENV V_VER="weekly.2021.39.1"

RUN apk add --no-cache build-base=0.5-r2 bash=5.1.0-r0 git=2.30.2-r0

WORKDIR /opt/vlang
RUN git clone https://github.com/vlang/v /opt/vlang && git checkout "${V_VER}" && make

ENV PATH=/opt/vlang:$PATH

WORKDIR /opt/app
COPY *.v .

RUN v -prod primes.v

FROM alpine:3.13

COPY --from=build /opt/app/primes /usr/local/bin/primes

ENTRYPOINT [ "primes" ]
