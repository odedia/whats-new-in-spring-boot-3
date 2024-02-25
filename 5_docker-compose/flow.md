Open the project in VScode

`code .`

start by commenting out `spring-boot-docker-compose` in `build.gradle`

Make sure nothing is running, then start the application. It should fail since there are is no Postgres container running:

```
docker compose down
gradle clean bootRun
```

Start the Postgres container and boot the app. Now it should work, but only because `application.yaml` points to the correct endpoint and credentials:
```
docker compose up -d
gradle clean bootRun
```
Shut down Postgres:
`docker compose down`

Change the port in `docker-compose.yaml` from `5432:5432` to `5433:5432`. Boot the application again. It will now fail because the app cannot connect to Postgres on port 5432:

```
docker compose up -d
gradle clean bootRun
```

Shut down Postgres:
`docker compose down`

Uncomment the `spring-boot-docker-compose` in build.gradle. Boot the application again. It will now connect to Postgres since it picks up the correct values from `docker-compose.yaml`, ignoreing `application.yaml`:

`gradle clean bootRun`

Uncomment the following in `applicatin.yaml`:

```
  datasource:
    url: "jdbc:postgresql://localhost:5432/demo-service-connection"
    username: "spring"
    password: "secret"
```
Boot the application again. It should still work, because again the application picks up the correct parameters on startup, ignoring what's set in `docker-compose.yaml`:

`gradle clean bootRun`

Run the Test class `CustomerRepositoryTests`, showing the Testcontainers integration

Rename `docker-compose.yaml` to `docker-compose.bk`, basically eliminating the Docker support.

Boot the application again, only this time using `bootTestRun`. The application will start correctly, using the configuration provided by Testcontainers and not `docker-compose.yaml`.

`gradle bootTestRun`

Rename `docker-compose.bk` back to `docker-compose.yaml`.
