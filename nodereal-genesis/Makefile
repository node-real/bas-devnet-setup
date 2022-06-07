.PHONY: clean
clean:
	rm -rf ./build

.PHONY: install
install:
	yarn

.PHONY: compile
compile:
	rm -rf build &&  cd ../genesis && yarn compile && node build-abi.js && cp -r build ../nodereal-genesis

.PHONY: test
test:
	yarn coverage

.PHONY: create-genesis
create-genesis:
	go run ./nodereal-genesis.go config.json genesis.json

.PHONY: all
all: clean install compile create-genesis
