SHELL := /bin/bash

VERSION ?= latest

include .env
export

.PHONY: deploy login pull up down status logs

deploy: login pull up
	@echo ""
	@echo "Deploy concluído!"
	@echo "Imagem: $(IMAGE_NAME):$(VERSION)"

login:
	@echo "Autenticando no Github Actions..."
	@echo "$(GHCR_TOKEN)" | docker login ghcr.io -u "$(GHCR_USER)" --password-stdin

pull:
	@echo "Baixando $(IMAGE_NAME):$(VERSION)..."
	@IMAGE_NAME="$(IMAGE_NAME)" VERSION="$(VERSION)" docker compose pull

up:
	@echo "Subindo a versão $(VERSION)..."
	@IMAGE_NAME="$(IMAGE_NAME)" VERSION="$(VERSION)" docker compose up -d

down:
	@IMAGE_NAME="$(IMAGE_NAME)" VERSION="$(VERSION)" docker compose down

status:
	@IMAGE_NAME="$(IMAGE_NAME)" VERSION="$(VERSION)" docker compose ps

logs:
	@IMAGE_NAME="$(IMAGE_NAME)" VERSION="$(VERSION)" docker compose logs -f