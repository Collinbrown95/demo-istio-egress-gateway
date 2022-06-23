IMAGE_NAME := diagrams

run: egress_gateway_deployed_components.png egress_gateway_behaviour.png

%.png: %.py build
	docker run -v $$(pwd)/:/tmp/ $(IMAGE_NAME) $<

build: Dockerfile
	docker build . -t $(IMAGE_NAME)