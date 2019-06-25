
oc login -u (user) https://(openshift-master-url)

Deploy application using S2i source from git
```
oc new-app jboss-webserver31-tomcat8-openshift:1.2~https://github.com/jboss-openshift/openshift-quickstarts.git#1.2 --context-dir=tomcat-websocket-chat --name=tomcat-websocket-chat
```

Deploy application using S2i source from local (build on server)
```
oc new-app jboss-webserver31-tomcat8-openshift:1.2 --code=. --name=tomcat-websocket-chat-local
oc start-build tomcat-websocket-chat-local --from-dir=. --follow
```

Deploy application using S2i binary from local (build on local)
```
oc new-app jboss-webserver31-tomcat8-openshift:1.2 --code=. --name=tomcat-websocket-chat-local-binary
mvn clean package
oc start-build tomcat-websocket-chat-local-binary --from-file=target/websocket-chat.war --follow
```

Delete application
```
oc delete dc/tomcat-websocket-chat-local-binary
oc delete bc/tomcat-websocket-chat-local-binary
oc delete svc/tomcat-websocket-chat-local-binary
oc delete route/tomcat-websocket-chat-local-binary
```
