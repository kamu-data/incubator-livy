# Kamu fork of Apache Livy

Kamu is building its own version of Livy for two reasons:
- As of this time latest Livy release does not contain Slaca 2.12 binaries, which are needed for Spark 3+ compatibility
- When working with Livy we want Apache Sedona types (GIS library) to be pre-registered inside the user's Spark session. Livy and Spark don't provide any hooks to do so, so we had to extend Livy to add them upon Spark session startup 
  - **TODO:** We shoud investigate if the recently added `spark.sql.extensions` config option can allow such auto-registration

## Building the fork

First clone the repo and make sure you're on `kamu` branch.

Clean command:
```sh
mvn clean -Pthriftserver -Pspark3 -Pscala-2.12 -DskipITs -DskipTests
```

Build command:
```sh
mvn package -Pthriftserver -Pspark3 -Pscala-2.12 -DskipITs -DskipTests
```
... this will take a while.

Package will be produced under:

```sh
./assembly/target/apache-livy-{version}-bin.zip
```
