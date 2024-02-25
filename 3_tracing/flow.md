Boot Zipkin by running:

`docker compose up -d`

Open the Zipkin UI:

http://127.0.0.1:9411/zipkin/

Build the two microservices:
`mvn clean package -DskipTests`

Boot both microservices in the background:
`java -jar message-service/target/message-service-0.0.1-SNAPSHOT.jar & java -jar billboard-client/target/billboard-client-0.0.1-SNAPSHOT.jar&`

Open the application:

http://localhost:8080

View the dependencies in zipkin

See how the random-quote#connection trace shows the author parameter. Find that in the code!
Show the tags

Review the following classes:

```
subl ./message-service/src/main/java/com/example/TracingMessageServiceApplication.java
subl ./message-service/src/main/java/com/example/MessageService.java
```

Stop the two microservices and docker compose:
```
fg, Ctrl+C
fg, Ctrl+C
docker compose down
```
