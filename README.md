# Demo: Sonarqube Community Branch Plugin

Sample scenario using [Sonarqube Community Branch Plugin](https://github.com/mc1arke/sonarqube-community-branch-plugin) in combination with Jenkins and GitLab.

## Setup Infrastructure: Jenkins, GitLab & SonarQube

URLs:

* Jenkins - http://localhost:8080
* GitLab - http://localhost:8000
* SonarQube - http://localhost:9000

### Docker Installation

```bash
export JENKINS_HOME=/srv/jenkins
export GITLAB_HOME=/srv/gitlab
export SONAR_HOME=/srv/sonar
export POSTGRESQL_HOME=/srv/postgresql

mkdir -p $JENKINS_HOME

mkdir -p $SONAR_HOME
wget -O $SONAR_HOME/sonarqube-community-branch-plugin-1.6.0.jar  https://github.com/mc1arke/sonarqube-community-branch-plugin/releases/download/1.6.0/sonarqube-community-branch-plugin-1.6.0.jar

sysctl -w vm.max_map_count=262144

docker-compose up -d --build
```

Uninstall/Cleanup Docker Installation:

```bash
docker-compose down

sudo rm -rf /srv/*
```

### Jenkins Settings

* Login: jenkins / jenkinspw

* GitLab API Token
  * Create API Token in [GitLab](http://localhost:8000/-/profile/personal_access_tokens): Scopes=api, read_api
  * Update credentials in [Jenkins](http://localhost:8080/credentials/store/system/domain/_/credential/gitlab_token/update)

* SonarQube
  * Create [Token](http://localhost:9000/admin/users)
  * Activate [Webhook](http://localhost:9000/admin/webhooks): URL=http://jenkins/sonarqube-webhook/
  * Update credentials in [Jenkins](http://localhost:8080/credentials/store/system/domain/_/credential/sonarqube_token/update)

## Requirements for Java Project

* Java JDK 11 (e.g. [AdoptOpenJDK 11](https://adoptopenjdk.net/installation.html#linux-pkg))
* [Maven](https://www.baeldung.com/install-maven-on-windows-linux-mac#2-installing-maven-on-ubuntu)

### Push Dummy Project

e.g. create new project in GitLab based on [Spring Template](https://gitlab.com/gitlab-org/project-templates/spring)
