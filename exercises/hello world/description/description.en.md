Write a Containerfile based on the Alpine base image that
- creates and switches to a user called `runner`
- sets his home dir `/home/runner` as the working directory
- copies the script `hello.sh` into the working directory
- has the labels `org.opencontainers.image.title` and `org.opencontainers.image.description` set
