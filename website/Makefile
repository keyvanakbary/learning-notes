# Default shell to use
SHELL := bash

# Reuse the same shell instance within a target. Requires make >= 3.82
.ONESHELL:

# Set bash to fail immediately (-e), to error on unset variables (-u) and to fail on piped commands (pipefail)
.SHELLFLAGS := -eu -o pipefail -c

# Delete any generated target on failure
.DELETE_ON_ERROR:

# Make flags
MAKEFLAGS += --warn-undefined-variables
MAKEFLAGS += --no-builtin-rules

COMPOSE = docker-compose

RUN_JEKYLL = $(COMPOSE) run -e JEKYLL_UID=$(shell id -u) -e JEKYLL_GID=$(shell id -g) jekyll

# Non file-generating targets
.PHONY: build server update

default: build

build:
	$(RUN_JEKYLL) jekyll build

server:
	$(COMPOSE) up

update:
	$(RUN_JEKYLL) bundle update
