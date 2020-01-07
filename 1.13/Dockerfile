# See https://github.com/golang/go/issues/14481
FROM golang:1.13-alpine AS race
WORKDIR /tmp/race
RUN apk --update -q --progress --no-cache add git g++
RUN git clone --single-branch https://llvm.org/git/compiler-rt.git . &> /dev/null
RUN git reset --hard fe2c72c59aa7f4afa45e3f65a5d16a374b6cce26 && \
    wget -q https://github.com/golang/go/files/3615484/0001-hack-to-make-Go-s-race-flag-work-on-Alpine.patch.gz -O patch.gz && \
    gunzip patch.gz && \
    patch -p1 -i patch
RUN cd lib/tsan/go && \
    ./buildgo.sh &> /dev/null


FROM golang:1.13-alpine

COPY --from=race /tmp/race/lib/tsan/go/race_linux_amd64.syso /usr/local/go/src/runtime/race/race_linux_amd64.syso

RUN apk add --no-cache git bash build-base openssh-client
