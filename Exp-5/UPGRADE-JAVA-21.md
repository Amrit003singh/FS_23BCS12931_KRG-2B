Upgrade notes for Java 21

This project has been updated to target Java 21.

What changed in the repo:

- Root `pom.xml` java.version set to 21 and `spring-boot-starter-parent` bumped to 3.2.12.
- `maven-compiler-plugin` configured to release 21 under pluginManagement in root POM.
- `system.properties` updated to `java.runtime.version=21` for Heroku.

Local steps to build and test (macOS, zsh):

1) Install JDK 21 (using SDKMAN or Homebrew). Example with SDKMAN:

```bash
# Install SDKMAN if you don't have it
curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"

# Install Java 21
sdk install java 21.0.0-tem
sdk use java 21.0.0-tem
```

Or using Homebrew + Temurin:

```bash
brew install temurin@21
# Make sure JAVA_HOME points to the JDK 21 installation
export JAVA_HOME="$(/usr/libexec/java_home -v 21)"
```

2) Install Maven if missing (Homebrew):

```bash
brew install maven
```

3) From the project root, run a build (skip tests on first pass):

```bash
mvn -U -DskipTests package
```

4) If the build fails, common fixes:
- Upgrade `javax.*` imports to `jakarta.*` (Spring Boot 3 uses Jakarta namespaces).
- Update any third-party libs that are not compatible with Java 21 or Spring Boot 3.
- Replace deprecated Spring APIs or update configuration keys.

Notes and next steps:

- I updated the POM to Spring Boot 3.2.12 which is compatible with Java 21. This is a major upgrade from 2.1.x and will likely require code changes.
- I recommend running the build locally and sharing any compile errors; I will help fix them iteratively.
- If you want, I can proceed to automatically apply `javax` -> `jakarta` package changes and other recipe-based migrations, but that is larger-scope work and may need careful review.

If you want me to continue with code migrations now, reply "continue" and I'll apply targeted changes (start with package migrations and dependency updates).