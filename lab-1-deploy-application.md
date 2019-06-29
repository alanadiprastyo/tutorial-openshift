Login into OpenShift
```
oc login -u (user) https://(openshift-master-url):8443
oc project (project-name)
```
Deploy application using Image docker from Docker Hub
```
oc tag --source=docker openshift/deployment-example:v2 deployment-example:latest
oc new-app deployment-example
```
Deploy application NodeJs using S2i from git
```
oc new-app --name=hello-world https://github.com/alanadiprastyo/nodejs-ex.git
```

Deploy application using S2i source from git
```
oc new-app jboss-webserver31-tomcat8-openshift:1.2~https://github.com/jboss-openshift/openshift-quickstarts.git#1.2 --context-dir=tomcat-websocket-chat --name=tomcat-websocket-chat
```

Deploy application using S2i source from local (build on server)  
Download source code from https://github.com/jboss-openshift/openshift-quickstarts/tree/1.2
```
cd openshift-quickstart/tomcat-websocket-chat
oc new-app jboss-webserver31-tomcat8-openshift:1.2 --code=. --name=tomcat-websocket-chat-local --build-env=MAVEN_MIRROR_URL=http://nexus3-dev-infra.imigrasi.go.id/repository/maven-public
oc start-build tomcat-websocket-chat-local --from-dir=. --follow
```

Deploy application using S2i binary from local (build on local)
```
oc new-app jboss-webserver31-tomcat8-openshift:1.2 --code=. --name=tomcat-websocket-chat-local-binary
mvn clean package
oc start-build tomcat-websocket-chat-local-binary --from-file=target/websocket-chat.war --follow
```

Deploy application using Dockerfile git
```
oc new-app https://github.com/jboss-dockerfiles/wildfly --name=dockerfile-wildfly --strategy=docker
```
Deploy application using Dockerfile local.  
Download docker file from https://raw.githubusercontent.com/jboss-dockerfiles/wildfly/master/Dockerfile
```
oc new-app . --name=dockerfile-wildfly-local --strategy=docker
oc start-build dockerfile-wildfly-local --from-dir=. --follow
```

Delete for each application
```
oc delete dc/dockerfile-wildfly-local
oc delete bc/dockerfile-wildfly-local
oc delete svc/dockerfile-wildfly-local
oc delete route/dockerfile-wildfly-local
oc delete is/dockerfile-wildfly-local
```
