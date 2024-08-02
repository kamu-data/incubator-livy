# Kamu fork of Apache Livy

Kamu is building its own version of Livy for two reasons:
- As of this time latest Livy release does not contain Slaca 2.12 binaries, which are needed for Spark 3+ compatibility
- When working with Livy we want Apache Sedona types (GIS library) to be pre-registered inside the user's Spark session. Livy and Spark don't provide any hooks to do so, so we had to extend Livy to add them upon Spark session startup 
  - **TODO:** We shoud investigate if the recently added `spark.sql.extensions` config option can allow such auto-registration

## Building the fork

To install Java & Scala we recommend using [SdkMan](https://sdkman.io/). Install the tool itself and then you can use following versions of components:

```bash
sdk use java  17.0.10-oracle
sdk use maven 3.9.6
sdk use sbt   1.9.8
sdk use scala 2.12.18
```

Install Python 2.7:

```sh
pyenv install 2.7.18
pyenv shell 2.7.18
pip install pytest-runner flake8
```

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
