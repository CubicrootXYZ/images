ARG GO_VERSION=1.21
ARG GOLANGCI_VERSION=1.54.2

FROM golang:${GO_VERSION}-bookworm

WORKDIR /app

RUN echo "deb http://archive.debian.org/debian buster-backports main" >> /etc/apt/sources.list.d/backport.list

RUN apt update && apt upgrade -y && \
    apt install -y git gcc docker && \
    apt install libolm-dev npm docker docker-compose -y

RUN go install github.com/CubicrootXYZ/openapi-code-sample-generator@latest \
    && go install honnef.co/go/tools/cmd/staticcheck@2021.1.2 \
    && go install github.com/swaggo/swag/cmd/swag@latest \
    && go install github.com/golangci/golangci-lint/cmd/golangci-lint@v${GOLANGCI_VERSION:-1.54.2}

RUN npm install redoc --save --legacy-peer-deps
RUN npm install redoc-cli

ENV PUSHBITS_HTTP_PORT="8080"
EXPOSE 8080  

RUN curl -fLo install.sh https://raw.githubusercontent.com/cosmtrek/air/master/install.sh \
    && chmod +x install.sh && sh install.sh && cp ./bin/air /bin/air

CMD air