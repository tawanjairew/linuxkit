.PHONY: tag push
default: push

ORG?=linuxkit
IMAGE=sshd
DEPS=Dockerfile etc/motd etc/ssh/sshd_config usr/bin/ssh.sh

HASH?=$(shell git ls-tree HEAD -- ../$(notdir $(CURDIR)) | awk '{print $$3}')

tag: $(DEPS)
	docker build --squash --no-cache --network=none -t $(ORG)/$(IMAGE):$(HASH) .

push: tag
	docker pull $(ORG)/$(IMAGE):$(HASH) || \
	docker push $(ORG)/$(IMAGE):$(HASH)
