ARG GO_VERSION=1.16

FROM golang:${GO_VERSION}-bullseye

WORKDIR /app

RUN echo "deb http://deb.debian.org/debian buster-backports main" >> /etc/apt/sources.list.d/backport.list

RUN apt update && apt upgrade -y && \
    apt install -y git gcc docker && \
    apt install libolm-dev npm -y

RUN go install github.com/CubicrootXYZ/openapi-code-sample-generator@latest \
    && go install honnef.co/go/tools/cmd/staticcheck@2022.1 \
    && go install github.com/swaggo/swag/cmd/swag@latest \
    && curl -sSfL https://raw.githubusercontent.com/golangci/golangci-lint/master/install.sh | sh -s -- -b $(go env GOPATH)/bin v1.46.2

RUN npm install redoc 
RUN npm install redoc-cli

ENV PUSHBITS_HTTP_PORT="8080"
EXPOSE 8080  

RUN curl -fLo install.sh https://raw.githubusercontent.com/cosmtrek/air/master/install.sh \
    && chmod +x install.sh && sh install.sh && cp ./bin/air /bin/air

CMD air