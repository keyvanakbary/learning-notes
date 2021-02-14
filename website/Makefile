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

# Non file-generating targets
.PHONY: build server update

default: build

build:
	$(COMPOSE) run jekyll jekyll build

server:
	$(COMPOSE) up

update:
	$(COMPOSE) run jekyll bundle update
