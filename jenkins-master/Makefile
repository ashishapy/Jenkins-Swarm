login:
	@docker login
network:
	@docker network create --driver overlay jenkins-ci
run:
	@docker service create --name jenkins-master \
	-e JENKINS_OPTS="--prefix=/jenkins" \
	--label com.df.notify=true \
	--label com.df.distribute=true \
	--label com.df.servicePath=/jenkins \
	--label com.df.port=8080 \
	--network jenkins-ci \
	--reserve-memory 300m \
	-p 8080:8080 -p 50000:50000 \
	ashishapy/jenkins-swarm-master
remove:
	@docker service rm jenkins-master
clean-images:
	@docker rmi $(docker images -q --filter="dangling=true")

# Label node
# $ docker node update --label-add env=jenkins-master <NODE>
