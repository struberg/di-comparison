# DI Containers Comparision

Comparing a simple app varieties on different DI containers.

## IntelliJ IDEA Setup

Go to "Preferences > Annotation Processors", and check "Enable Annotation
Processing".

## "Benchmark"

```
# Warmup build
$ mvn clean package

# Measure assembly time with "-o" to ensure loading dependencies over
# the network does not interfere...
$ mvn clean package -o

# Get the file sizes
$ find . -name '*.jar' |xargs ls -l |grep -v original |grep -v common

# Execution time
$ time java -jar ./cayennedi/target/cayennedi-1.0-SNAPSHOT.jar
$ time java -jar ./dagger/target/dagger-1.0-SNAPSHOT.jar
$ time java -jar ./guice/target/guice-1.0-SNAPSHOT.jar
$ time java -jar ./spring/target/spring-1.0-SNAPSHOT.jar
$ time java -jar ./springboot/target/springboot-1.0-SNAPSHOT.jar
```

## Results

|DI|Compile/Package Time, ms|Jar with Dependencies, KB|Exec time, ms|
|----|-----|-----|----|
|Dagger|1297|51|121|
|Cayenne DI|91|79|180|
|Guice|477|3440|358|
|Spring|468|3545|506|
|Spring Boot|441|6993|1549|
