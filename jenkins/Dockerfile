FROM ubuntu:quantal
MAINTAINER mharj
RUN export DEBIAN_FRONTEND=noninteractive
ENV DEBIAN_FRONTEND noninteractive
ADD http://pkg.jenkins-ci.org/debian/jenkins-ci.org.key /tmp/jenkins-ci.org.key
RUN mkdir -p /var/run/jenkins
RUN cat /tmp/jenkins-ci.org.key | apt-key add -
RUN echo deb http://pkg.jenkins-ci.org/debian binary/ > /etc/apt/sources.list.d/jenkins.list
RUN apt-get install -y software-properties-common
RUN add-apt-repository ppa:webupd8team/java
RUN echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections
RUN echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections
RUN apt-get update
RUN apt-get install -y oracle-jdk7-installer jenkins
RUN apt-get clean all
ENV JENKINS_HOME /var/lib/jenkins
USER jenkins
EXPOSE 8080
CMD JENKINS_HOME=/var/lib/jenkins /usr/bin/java -jar /usr/share/jenkins/jenkins.war --webroot=/var/cache/jenkins/war --httpPort=8080 --ajp13Port=-1
