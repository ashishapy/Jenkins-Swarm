FROM jenkins:2.32.1-alpine

MAINTAINER Ashish Pandey "ashishapy@gmail.com"


# root user
USER root

# Install packages
RUN apk update && apk upgrade \
	&& apk add \
		ca-certificates \
		openssl \
		tar \
		py-pip \
		make \
	&& rm -rf /var/cache/apk/*

# Create Jenkins user and log Folder
RUN mkdir /var/log/jenkins \
	&& mkdir /var/cache/jenkins \
	&& chown -R jenkins:jenkins /var/log/jenkins \
	&& chown -R jenkins:jenkins /var/cache/jenkins \
	# add jenkins user to the group with default group id 50
	&& addgroup -g 50 docker \
	# TODO: use ARG for group name, instead of hardcoding group name
	&& adduser jenkins docker

# Docker entrypoint script
COPY scripts/docker-entrypoint.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/docker-entrypoint.sh

# Change to jenkins user
USER jenkins

# Set default options
ENV JAVA_OPTS="-Djava.util.logging.config.file=/var/jenkins_home/log.properties"
ENV JENKINS_OPTS="--logfile=/var/log/jenkins/jenkins.log --webroot=/var/cache/jenkins/war"

# Run docker and jenkins entrypoint scripts
ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["/bin/tini", "--", "/usr/local/bin/jenkins.sh"]