This is a Springboot application which can be run both locally and in the cloudfoundry platform.

If run locally, update the _application.properties_ in order to let the application connect to a running rabbitmq server.

If target to run the application in the cloudfoundry platform, do the following.

1. Navigate to the directory, build the package using:

```text
    mvn pacakge -Dmaven.test.skip = true
```

2. Provision a rabbitmq service and name it _spring-rabbitmq_, this is specified in the _manifest.yml_

3. Do the cf push to push the application to the cf platform.

**How to publish a message.**

The app contains one url: {url_to_app}/message, it's a POST method, so if you want to publish a message, do:

```text
curl -H "Accept: application/json" -H "Content-type: application/json" -X POST -d '{"message": "message for queue"}' http://<baseurl>/message
```

Check the application log to verify whether the consumer received the message or not, in theory, the application should 
contains a entry like:

```text
2018-12-19T13:19:22.636+08:00 [APP/PROC/WEB/0] [OUT] Received <message for queue>
```