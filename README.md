# Shippable Spring Boot war with React UI

## React UI

The UI is separated from the java src, and can be run without the backend for quicker frontend development (real-time code changes). To run just the frontend:

```bash
cd ui/
npm start
```
Served at http://localhost:3000/

## Java Web App

This project is a sandbox for Spring Boot app(s) with Gradle

Current Goals
- Make a spring boot app that works in tomcat as a deployable war, **without** using any xml configuration
- Use a port other than 8080, ex. 8090

### Running the app

Two options, both served at http://localhost:8090/spring-boot-react/

1. As a deployable war in a tomcat instance with cargo plugin (check cargo config for outputFile location, as it logs separately):

```bash
./gradlew cargoRunLocal -i
```

2. As a Spring Boot app (backend only - no UI):

```bash
./gradlew bootRun
```

Helpful Resources:

- [Spring Boot Tutorial](https://spring.io/guides/gs/spring-boot/)
- [Spring MVC Tutorial](https://spring.io/guides/gs/serving-web-content/)
- [Create a Deployable War File](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#howto-create-a-deployable-war-file)
- [Fix for javax/el/ELManager ClassNotFound](https://stackoverflow.com/a/49414569)
- [Packaging Executable Wars](https://docs.spring.io/spring-boot/docs/current/gradle-plugin/reference/html/#packaging-executable-wars)
- [Gradle Java Web App Tutorial (newer Gradle conventions)](https://guides.gradle.org/building-java-web-applications/)