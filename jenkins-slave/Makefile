login:
    @docker login
run:
# export USER, PASSWORD, JENKINS_MASTER
    @docker service create --name jenkins-agent \
    -e COMMAND_OPTIONS="-master \
    http://$JENKINS_MASTER:8080/jenkins \
    -username $USER -password $PASSWORD \
    -labels 'docker' -executors 5" \
    --mount "type=bind,source=/var/run/docker.sock,target=/var/run/docker.sock" \
    --mount "type=bind,source=/workspace,target=/workspace" \
    --network jenkins-ci \
    ashishapy/jenkins-swarm-agent
remove:
	@docker service rm jenkins-agent
clean-images:
	@docker rmi $(docker images -q --filter="dangling=true")