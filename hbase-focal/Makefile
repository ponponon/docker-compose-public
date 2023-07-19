NAME = ponponon/hbase
VERSION = 2.4.17

.PHONY: build up stop logs

build:  docker-build
up: docker-compose-up
stop: docker-compose-stop
logs: docker-compose-logs

docker-build:
	docker build -t "${NAME}:${VERSION}" .

docker-compose-up:
	docker-compose up -d

docker-compose-stop:
	docker-compose stop

docker-compose-logs:
	docker-compose logs --tail=100 -f
