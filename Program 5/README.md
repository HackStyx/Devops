##  **1. Create a New Gradle Project**

1. Open the terminal and create a new directory:

    ```bash
    mkdir MyGradleApp
    cd MyGradleApp
    ```

2. Initialize the Gradle project:

    ```bash
    gradle init --type java-application
    ```

---

##  **2. Project Structure**

The project structure will be generated as follows:

```
MyGradleApp/
├── build.gradle
├── gradle/
├── gradlew
├── gradlew.bat
├── settings.gradle
└── src/
    ├── main/
    │   └── java/
    │       └── App.java
    └── test/
        └── java/
            └── AppTest.java
```

---

##  **3. Update `build.gradle` File (if not exists)**

Open the `build.gradle` file and modify its content:

```gradle
// Apply the java plugin to add support for Java
apply plugin: 'java'

// Apply the application plugin to add support for building an application
apply plugin: 'application'

// Specify the repository
repositories {
    jcenter()
}

// Define project dependencies
dependencies {
    implementation 'com.google.guava:guava:23.0'
    testImplementation 'junit:junit:4.12'
}

// Define the main class for the application
mainClassName = 'App'

// Custom task
task display {
    doLast {
        println 'hello DevOps Class'
    }
}
```

---

##  **4. Modify `App.java`**

Navigate to `src/main/java/` and update `App.java` with the following content:

```java
public class App {
    public static void main(String[] args) {
        System.out.println("Hello, Gradle Application!");
    }
}
```

---

##  **5. Build the Project**

Run the build command to compile the project:

```bash
gradle build
```

- This will generate the `build/` directory with compiled classes and other resources.

---

##  **6. Run the Application**

To run the application:

```bash
gradle run
```

**Expected Output:**

```
Hello, Gradle Application!
```

---

##  **7. Execute the Custom Task**

To run the custom `display` task:

```bash
gradle display
```

**Expected Output:**

```
hello DevOps Class
```

---

##  **8. Troubleshooting and Cleanup** (Optional)

- Ensure Gradle is installed properly by checking the version:

    ```bash
    gradle -v
    ```

- If any dependency fails, verify the `build.gradle` file for syntax errors.

- Clean the build directory using:

    ```bash
    gradle clean
