builder:

.PHONY:	builder-amd64 builder-arm64v8 custom-jenkins-docker

builder-amd64:
	cd amd64 && docker build -t builder-amd64 .

builder-arm64v8:
	cd arm64v8 && docker build -t builder-arm64v8 .

custom-jenkins-docker:
	cd jendock && docker build -t custom-jenkins-docker .
