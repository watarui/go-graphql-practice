FROM golang:latest

WORKDIR /app

RUN apt-get update && apt-get install -y \
  jq \
  sqlite3 libsqlite3-dev \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

COPY go.mod ./
COPY go.sum ./

RUN go mod download

# RUN go get -u github.com/go-sql-driver/mysql

RUN go install github.com/cosmtrek/air@latest
RUN go install github.com/go-delve/delve/cmd/dlv@latest
RUN go install honnef.co/go/tools/cmd/staticcheck@latest
RUN go install golang.org/x/tools/gopls@latest
RUN go install github.com/swaggo/swag/cmd/swag@latest
RUN go install golang.org/x/tools/cmd/godoc@latest
RUN go install github.com/99designs/gqlgen@latest

RUN curl -sSfL https://raw.githubusercontent.com/golangci/golangci-lint/master/install.sh | sh -s -- -b $(go env GOPATH)/bin

ENTRYPOINT ["tail", "-F", "/dev/null"]
