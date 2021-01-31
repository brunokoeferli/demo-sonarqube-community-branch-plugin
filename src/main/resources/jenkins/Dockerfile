FROM jenkins/jenkins:lts

ENV JAVA_OPTS -Djenkins.install.runSetupWizard=false
ENV CASC_JENKINS_CONFIG /jenkins/casc.yaml

# Install plugins
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN jenkins-plugin-cli -f /usr/share/jenkins/ref/plugins.txt

# Configuration as Code: https://github.com/jenkinsci/configuration-as-code-plugin
COPY casc.yaml /jenkins/casc.yaml