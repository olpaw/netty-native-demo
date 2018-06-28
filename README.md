# Instant Netty startup using SubstrateVM Native Image Generation

This is a variant of https://github.com/cstancu/netty-native-demo where instead of using a [GraalVM](http://graalvm.org/) release the master version of SubstrateVM is used instead. Additionally we are using the native-image maven-plugin to allow image building directly from maven.

### Setting up SubstrateVM development

To set up your development environment first perform the steps described in [Substrate VM - Quick start](https://github.com/oracle/graal/tree/master/substratevm#quick-start). After running 
```
$ mx build
```

in the substratevm subdirectory you also need to run:
```
$ mx maven-plugin-install
```
 
This will install the native-image maven-plugin into your local maven repository. After running the command you will see something like:
```
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 3.335 s
[INFO] Finished at: 2018-06-28T15:18:43+02:00
[INFO] Final Memory: 40M/1009M
[INFO] ------------------------------------------------------------------------

Use the following plugin snippet to enable native-image building for your maven project:

<plugin>
    <groupId>com.oracle.substratevm</groupId>
    <artifactId>native-image-maven-plugin</artifactId>
    <version>feef79390e56345a15937dae9350898fa1f24299-SNAPSHOT</version>
    <executions>
        <execution>
            <goals>
                <goal>native-image</goal>
            </goals>
            <phase>package</phase>
        </execution>
    </executions>
</plugin>
```

The only thing left to do is either to replace the `${substratevm.version}` occurrences in this project pom or instead just run:

```
$ mvn -Dsubstratevm.version=feef79390e56345a15937dae9350898fa1f24299-SNAPSHOT package
```

After running `mvn package` you will find the netty native-image executable in `target/netty-svm-http-server`. If you want to test the image please refer to the original README file.
