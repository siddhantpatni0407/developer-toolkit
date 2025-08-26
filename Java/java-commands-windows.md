# ☕ Java Commands & Setup Guide (Windows)

A comprehensive reference for Java development on Windows, including environment setup, compiling, running programs, and advanced tips for managing projects with Maven and Gradle.

---

## 🛠 Environment Setup (Windows)

| Command / Setting | Description |
|-------------------|-------------|
| `java -version` | Check installed Java version in Command Prompt or PowerShell. |
| `javac -version` | Check Java compiler version. |
| `echo %JAVA_HOME%` | Display the current `JAVA_HOME` environment variable. |
| **Set `JAVA_HOME` environment variable:** |  
> 1. Open **System Properties** → **Advanced** → **Environment Variables**.  
> 2. Under **System variables**, click **New** (or edit if exists).  
> 3. Set variable name as `JAVA_HOME` and variable value to your JDK path (e.g., `C:\Program Files\Java\jdk-17`).  
> 4. Add `%JAVA_HOME%\bin` to your `Path` variable.  
> 5. Restart Command Prompt or PowerShell for changes to take effect. |
| `java -jar <file.jar>` | Run an executable JAR file. |

---

## 📄 Compiling & Running Java Programs

| Command | Description |
|---------|-------------|
| `javac MyClass.java` | Compile a Java source file into bytecode `.class` files. |
| `java MyClass` | Run the compiled Java program (class with `main` method). |
| `javac -d bin src\*.java` | Compile all Java files from `src` folder and output `.class` files to `bin` folder. |
| `java -cp bin MyClass` | Run Java program specifying the classpath. |

---

## 📦 Managing Dependencies & Build Tools

### Maven (Windows)

| Command                                   | Description                                                    |
|-------------------------------------------|----------------------------------------------------------------|
| `mvn -v`                                  | Check Maven version (requires Maven installed and in `Path`).  |
| `mvn clean`                               | Clean the project build (remove `target` directory).           |
| `mvn compile`                             | Compile the source code of the project.                         |
| `mvn test`                                | Run tests using the configured testing framework (e.g., JUnit).|
| `mvn package`                             | Package compiled code into a JAR/WAR file.                      |
| `mvn install`                             | Install the built artifact into the local Maven repository.    |
| `mvn deploy`                              | Deploy the built artifact to a remote repository.               |
| `mvn validate`                            | Validate the project is correct and all necessary information is available. |
| `mvn verify`                              | Run any checks to verify the package is valid and meets quality criteria. |
| `mvn dependency:tree`                     | Display project dependency tree.                               |
| `mvn dependency:analyze`                  | Analyze dependencies and identify unused or undeclared ones.  |
| `mvn help:effective-pom`                  | Show the effective POM after inheritance and interpolation.    |
| `mvn site`                                | Generate a site documentation for the project.                  |
| `mvn clean install -DskipTests`           | Clean and install the project skipping tests.                   |
| `mvn versions:display-dependency-updates` | Check for newer versions of dependencies.                      |
| `mvn release:prepare`                     | Prepare a release (tag the release, update versions).           |
| `mvn release:perform`                     | Perform the release (deploy the artifacts).                     |

---

### Gradle (Windows)

| Command                               | Description                                                    |
|-------------------------------------|----------------------------------------------------------------|
| `gradle -v`                         | Check Gradle version (requires Gradle installed and in `Path`).|
| `gradle init`                       | Initialize a new Gradle project.                               |
| `gradle clean`                      | Delete build directory to clean the project.                   |
| `gradle build`                      | Compile, test, and package the project.                        |
| `gradle assemble`                   | Compile and package without running tests.                     |
| `gradle test`                      | Run tests.                                                     |
| `gradle check`                     | Run all verification tasks (tests, static analysis).           |
| `gradle run`                       | Run the main class of the application (if configured).         |
| `gradle tasks`                     | List all available tasks in the project.                       |
| `gradle dependencies`              | Show the dependency tree of the project.                       |
| `gradle dependencyInsight --dependency <dep>` | Detailed insight into a specific dependency.           |
| `gradle jar`                       | Build the JAR file for the project.                            |
| `gradle publish`                   | Publish artifacts to a remote repository (requires config).    |
| `gradle wrapper`                   | Generate Gradle Wrapper scripts (gradlew.bat, gradlew).        |
| `gradle --refresh-dependencies`   | Refresh dependencies and ignore cached ones.                   |
| `gradle --daemon`                  | Run Gradle with daemon enabled for faster builds.              |
| `gradle --offline`                 | Run Gradle without accessing network resources.                 |
| `gradle --parallel`                | Build projects in parallel when possible.                       |
| `gradle build --scan`              | Build the project and generate a build scan report.            |

---

> 💡 **Note:**  
> Replace `gradle` with `./gradlew` or `gradlew.bat` when using the Gradle Wrapper in Windows projects, to ensure consistent Gradle versions.

---

If you'd like, I can prepare this in full file format or add sample usage examples for some of the commands!


---

## 🧪 Running Tests

| Command | Description |
|---------|-------------|
| `java -jar junit-platform-console-standalone.jar -cp . --scan-classpath` | Run JUnit tests from command line. |
| `mvn test` | Run tests with Maven. |
| `gradle test` | Run tests with Gradle. |

---

## 🔧 Useful Java Commands

| Command | Description |
|---------|-------------|
| `javadoc -d docs MyClass.java` | Generate JavaDoc API documentation. |
| `jps` | List running Java processes (Java Process Status Tool). |
| `jstat -gc <pid>` | Monitor garbage collection of a running JVM process. |
| `jmap -heap <pid>` | Show heap info of a running JVM process. |
| `jstack <pid>` | Dump thread stack traces (helpful for debugging). |

---

## 🧠 Tips for Java Development on Windows

- Set `JAVA_HOME` and update your `Path` environment variable properly to avoid "command not found" errors.
- Use **PowerShell** or **Command Prompt**; PowerShell supports more advanced scripting.
- Use Maven or Gradle for dependency and build management.
- Write and run unit tests frequently.
- Use VisualVM (bundled with JDK) or Java Mission Control for monitoring JVM performance.

---

## 🌐 External References

- [Oracle Java Documentation](https://docs.oracle.com/en/java/)
- [Maven Official Site](https://maven.apache.org/)
- [Gradle Official Site](https://gradle.org/)
- [JUnit 5 User Guide](https://junit.org/junit5/docs/current/user-guide/)

---

## 📌 Recommended Basic Workflow (Windows)

### 🔽 Clone your project and navigate:

```powershell
git clone <url>
cd <repo>
