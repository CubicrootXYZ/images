FROM golang:1.16.0-buster

WORKDIR /app

RUN echo "deb http://deb.debian.org/debian buster-backports main" >> /etc/apt/sources.list.d/backport.list

RUN apt update && apt upgrade -y && \
    apt install -y git gcc npm && \
    apt install libolm-dev/buster-backports -y

RUN go install github.com/CubicrootXYZ/openapi-code-sample-generator@latest \
    && go install honnef.co/go/tools/cmd/staticcheck@latest \
    && go install github.com/swaggo/swag/cmd/swag@latest

RUN npm install redoc 

ENV PUSHBITS_HTTP_PORT="8080"
EXPOSE 8080  

RUN curl -fLo install.sh https://raw.githubusercontent.com/cosmtrek/air/master/install.sh \
    && chmod +x install.sh && sh install.sh && cp ./bin/air /bin/air

CMD air