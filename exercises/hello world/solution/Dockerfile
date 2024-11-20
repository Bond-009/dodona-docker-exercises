FROM alpine:3.20

RUN useradd -ms /bin/bash runner
USER runner
WORKDIR /home/runner
COPY hello.sh .

LABEL org.opencontainers.image.title="Hello" \
      org.opencontainers.image.description="Says hello world"
