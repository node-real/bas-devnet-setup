.PHONY: clean
clean:
	rm -rf ./build
var:
 BINARY_NAME=create-genesis

.PHONY: install
install:
	yarn

.PHONY: compile
compile:
	rm -rf build &&  cd ../genesis && yarn compile && node build-abi.js && cp -r build ../nr-genesis

.PHONY: create-genesis
create-genesis:
	go run ./nr-create-genesis.go nr-config.json genesis.json

build-all:
	GOARCH=amd64 GOOS=darwin go build -o ${BINARY_NAME}-darwin nr-create-genesis.go
	GOARCH=amd64 GOOS=linux go build -o ${BINARY_NAME}-linux nr-create-genesis.go
	GOARCH=arm64 GOOS=darwin go build -o ${BINARY_NAME}-darwin-arm64 nr-create-genesis.go

build-linux:
	GOARCH=amd64 GOOS=linux go build -o ${BINARY_NAME}-linux nr-create-genesis.go

.PHONY: all
all: clean install compile create-genesis build-linux
