FROM golang:1.16

ENV GOPATH /go
ENV GO111MODULE on

WORKDIR /app
COPY ./app /app

# 必要なパッケージなどをインストールする
RUN apt-get update && \
    apt-get upgrade -y

RUN go get -u github.com/cosmtrek/air

# go modulesを利用してライブラリを導入する
RUN go mod init main \
  && go mod tidy \
  && go build


# install revel and revel-cli
RUN go get github.com/jinzhu/gorm && \
    go get github.com/go-sql-driver/mysql && \
    go get github.com/garyburd/redigo/redis && \
    go get github.com/patrickmn/go-cache && \
    go get github.com/bradfitz/gomemcache/memcache



# ginは8080ポートで実行される
ENV CGO_ENABLED=0 \
  GOOS=linux \
  GOARCH=amd64
EXPOSE 8080

CMD ["go", "run", "main.go"]