# Build the hello-app-go example

# Usage:
#   [VERSION=v3] [REGISTRY="staging-k8s.gcr.io"] make build
VERSION?=v1
REGISTRY?=docker.io/basdemirs

release: clean build push clean

# builds a docker image that builds the app and packages it into a minimal docker image
build:
	docker build -t ${REGISTRY}/hello-app:${VERSION} .

# push the image to an registry
push:
	docker -- push ${REGISTRY}/hello-app:${VERSION}

# remove previous images and containers
clean:
	docker rm -f ${REGISTRY}/hello-app:${VERSION} 2> /dev/null || true

.PHONY: release clean build push