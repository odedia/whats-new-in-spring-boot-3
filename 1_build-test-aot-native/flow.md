Review the gradle tasks related to AOT:

`gradle tasks --all | grep Aot`

Remove the build folder:
`rm -rf build`

Build the project (also runs `processAot`):
`gradle clean build`

View the generated Aot Resources:

`subl ./build/generated/aotResources/META-INF/native-image/com.example/build-test-aot-native`

View the RuntimeHints file:

`subl ./src/main/java/com/example/aot/BuildTestAotNativeRuntimeHints.java`

Boot the application:
`gradle bootRun`

Open the REST api in a browser:

`http://localhost:8080/hello?mode=bean`

Copy the PID from the Spring boot logs, and check the memory consumption:

`ps -o rss= -p <PID> | awk '{print $1 / 1024}'`

Run a native compilation:
`gradle clean nativeCompile`

Josh Long's request for elevator music during compilation!
`https://github.com/oracle/graal/issues/5327`

Run the native executable really fast:
`./build/native/nativeCompile/build-test-aot-native`

Open the REST api in a browser:

`http://localhost:8080/hello?mode=bean`

Check the memory consumption again with the new PID:

`ps -o rss= -p <PID> | awk '{print $1 / 1024}'`
