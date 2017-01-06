build:
	@docker build -t ashishapy/jenkins-swarm-master .
login:
	@docker login
push:
	@docker push ashishapy/jenkins-swarm-master
run:
	@docker service create -p 8080:8080 -p 50000:50000 --name=jenkins-master \
	    --constraint node.labels.env==jenkins-master \
		ashishapy/jenkins-swarm-master
remove:
	@docker service rm jenkins-master
clean-images:
	@docker rmi $(docker images -q --filter="dangling=true")
