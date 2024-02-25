Make sure in `application.properties` the setting is:

`spring.threads.virtual.enabled=false`

Boot with a lot of cores and memory (this work ok for an M1 Max Macbook Pro):

`SPRING_BOOT_RUN_JVM_ARGUMENTS="-XX:ActiveProcessorCount=12 -Xmx4096m" mvn spring-boot:run`

In a second terminal, run Apache Bench:

`ab -n 5000 -c 10 http://localhost:8080/vets.html`

Run it again. At some point you should notice it "chokes".

Stop the app. Change the setting to:

`spring.threads.virtual.enabled=true`

Boot the application again:

`SPRING_BOOT_RUN_JVM_ARGUMENTS="-XX:ActiveProcessorCount=12 -Xmx4096m" mvn spring-boot:run`

Becnmark again:

`ab -n 5000 -c 10 http://localhost:8080/vets.html`

If it shows it stuck on second run, do realize that there's no magic here - there is a lot more GC going on, and both client and server run on the same machine.

Stop the app.

Let's see Checkpoint Restore in action. Boot the app:

`mvn spring-boot:run`

How how long it takes to load - usually around 3-4 seconds. Not bad!

Open checkpoint.sh. Review the script. Notice how the docke build essentially "waits" for the JVM to warm up before taking a snapshot of the running application.

Run the script:

`./checkpoint.sh`

Hit Enter after the application is booted.

See two images related to crac in the locak docker daemon:

`docker images | grep crac`

Open restore.sh. It is basically a `docker run` command with some additional paramters. Run the script:

`./restore.sh`

Startup time should now be less than 100ms. The only "penalty" compared to GraalVM is excessive memory usage, like any JVM. Another caveat is to make sure all I/O is closed when creating the checkpoint. However, the benefit is that this is a regular JVM with all the optimizations you've come to expect at runtime.
