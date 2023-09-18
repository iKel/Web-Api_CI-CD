app_name = webflow-frontend
acc = $(shell aws sts get-caller-identity --query Account --output text)

stage = dev
include configs/$(stage)

build:
	docker build -t $(app_name):$(v) .
login:
	aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin $(acc).dkr.ecr.us-east-1.amazonaws.com

push: login
	docker tag $(app_name):$(v) $(acc).dkr.ecr.us-east-1.amazonaws.com/$(app_name):$(v)
	docker push $(acc).dkr.ecr.us-east-1.amazonaws.com/$(app_name):$(v)
deploy:
	helm upgrade --install $(app_name) app-front/ --namespace $(namespace) --create-namespace \
		--set ft.app.name=$(app_name) \
		--set replica=$(replicas) \
		--set image.repo=$(acc).dkr.ecr.us-east-1.amazonaws.com/$(app_name) \
		--set version=$(v) \
		--set port=80 \
		--set hostname=$(app_hostname)