# Shippable Spring Boot war with React UI

## About

This project came from the desire to have a React app that can be built and tested as an isolated ui project, but also configured to be embedded into a deployable war.

- [Initial Build](#initial-build)
- [React UI](#react-ui)
- [Java Web App](#java-web-app)
- [Dev Workflow](#dev-workflow)
- [Helpful Resources](#helpful-resources)

## Initial Build

For now, this project requires you to have npm installed. Not sure if you have it? Run `npm -v`. If you have npm, a version will display.

To build, run the following command from the root directory of this repo:

```bash
./gradlew build
```

## React UI

The UI is separated from the java src, and can be run without the backend for quicker frontend development (real-time code changes). To run just the frontend:

```bash
cd ui/
npm start
```
Served at http://localhost:3000/

## Java Web App

Current Goals
- Make a spring boot app that works in tomcat as a deployable war, **without** using any xml configuration
- Use a port other than 8080, ex. 8090

>For the original Spring Boot web app, see the [sample-web-app](https://gitlab.com/tveal/sample-web-app).

### Running the app

Two options, both served at http://localhost:8090/spring-boot-react/

_Run from the root directory_

1. As a deployable war in a tomcat instance with cargo plugin (check cargo config for outputFile location, as it logs separately):

    ```bash
    ./gradlew cargoRunLocal -i
    ```

2. As a Spring Boot app (backend only - no UI):

    ```bash
    ./gradlew bootRun
    ```

### War Name and Root Context

The war uses the `project.name` property for it's name. For this project, it's set in __settings.gradle__, as:

```properties
rootProject.name = 'spring-boot-react'
```

This Gradle project is also configured to use `project.name` as the root context for running the war. This way, if you clone this repo to a different root folder name (or rename the root folder), it will still use `rootProject.name` for the war and root context.

## Dev Workflow

Some useful commands for on-going dev work

From ui directory:
```bash
# serve ui for active changes
npm start

# manually running the ui build
npm run build

# update your node_modules from the package.json
npm install

# clean ui build output
../gradlew clean
```

From root directory
```bash
# clean previous build output and build war
./gradlew clean build

# force rebuild of ui and assemble java web app before running war
./gradlew clean cargoRunLocal -i

# run just the backend (a faster startup if you need to test api endpoints)
./gradlew bootRun
```

## Helpful Resources:

- [Spring Boot Tutorial](https://spring.io/guides/gs/spring-boot/)
- [Spring MVC Tutorial](https://spring.io/guides/gs/serving-web-content/)
- [Create a Deployable War File](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#howto-create-a-deployable-war-file)
- [Fix for javax/el/ELManager ClassNotFound](https://stackoverflow.com/a/49414569)
- [Packaging Executable Wars](https://docs.spring.io/spring-boot/docs/current/gradle-plugin/reference/html/#packaging-executable-wars)
- [Gradle Java Web App Tutorial (newer Gradle conventions)](https://guides.gradle.org/building-java-web-applications/)