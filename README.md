# party-challange-dmn project

This project uses Quarkus, the Supersonic Subatomic Java Framework.

If you want to learn more about Quarkus, please visit its website: https://quarkus.io/ .

## Running the application in dev mode

You can run your application in dev mode that enables live coding using:
```shell script
./mvnw compile quarkus:dev
```

## Packaging and running the application

The application can be packaged using:
```shell script
./mvnw package
```
It produces the `party-challange-dmn-1.0.0-SNAPSHOT-runner.jar` file in the `/target` directory.
Be aware that it’s not an _über-jar_ as the dependencies are copied into the `target/lib` directory.

If you want to build an _über-jar_, execute the following command:
```shell script
./mvnw package -Dquarkus.package.type=uber-jar
```

The application is now runnable using `java -jar target/party-challange-dmn-1.0.0-SNAPSHOT-runner.jar`.

## Creating a native executable

You can create a native executable using: 
```shell script
./mvnw package -Pnative
```

Or, if you don't have GraalVM installed, you can run the native executable build in a container using: 
```shell script
./mvnw package -Pnative -Dquarkus.native.container-build=true
```

You can then execute your native executable with: `./target/party-challange-dmn-1.0.0-SNAPSHOT-runner`

If you want to learn more about building native executables, please consult https://quarkus.io/guides/maven-tooling.html.

## To run this example

You can see the swagger page by accessing the following endpoint `http://localhost:8080/q/swagger-ui`. The rule name is *PartyChallenge* and you can run it through the swagger page.

Or you can run the rule from terminal:

```bash
curl -X POST "http://localhost:8080/PartyChallenge" \
  -H  "accept: application/json" \
  -H  "Content-Type: application/json" \
  -d "{\"Guest\":{\"birthdate\":\"1980-01-01\",\"name\":\"Guilherme\"},\"Planned Date\":\"2021-10-25\"}"
```

In any case the body of request is:

```json
{
  "Guest": {
    "birthdate": "1980-01-01",
    "name": "Guilherme"
  },
  "Planned Date": "2021-10-25"
}
```

## The business Rule

In this challenge, you’re requested to create a decision service that helps a party owner to decide whether or not a guest can join the party.

- Goal: Return true or false, depending on the fact that a Guest can join a party on a specific Planned Date.

- Party rules:

  - To make a decision on whether a specific Guest Can Party, the party owner will inform:

    - A Guest, with name (text) and birthdate ("YYYY-MM-DD" format).

    - A Planned Date for this party ("YYYY-MM-DD" format).

  - Only guests that are 18 years or more can party.

  - There is a Banned guests list, that defines that "Chucky" and "Carrie" can’t party.