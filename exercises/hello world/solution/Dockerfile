FROM alpine:3.20

RUN adduser -Sh /home/runner runner
USER runner
WORKDIR /home/runner
COPY hello.sh .

LABEL org.opencontainers.image.title="Hello" \
      org.opencontainers.image.description="Says hello world"
