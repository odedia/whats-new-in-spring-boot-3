Start Prometheus in the background:
`docker compose up -d`

Show MetricsApplication, OrderService classes in VScode.
Note how all observability is not under the `io.micrometer` package and responsibility. No more Spring Cloud Sleuth.

Boot the application:
`mvn spring-boot:run`

Shoe the following URLs:

http://localhost:8080
http://localhost:8080/actuator/metrics
http://localhost:8080/actuator/metrics/orders.flagged
http://localhost:8080/actuator/prometheus

View the prometheus UI:
http://localhost:9090/

Search for:
`orders_placed_total`

