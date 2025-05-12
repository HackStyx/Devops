## 1. Create a New Maven Project

```bash
mvn archetype:generate -DgroupId=com.example -DartifactId=MyMavenGuavaApp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

---

## 2. Navigate to the Project Directory

```bash
cd MyMavenGuavaApp
```

---

## 3. Update `pom.xml` File

Replace the content of the `pom.xml` file with the following:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
         http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>MyMavenGuavaApp</artifactId>
    <packaging>jar</packaging>
    <version>1.0-SNAPSHOT</version>
    <name>MyMavenGuavaApp</name>
    <url>http://maven.apache.org</url>

    <properties>
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>
    </properties>

    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>3.8.1</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>com.google.guava</groupId>
            <artifactId>guava</artifactId>
            <version>33.4.0-jre</version>
        </dependency>
        <dependency>
            <groupId>commons-io</groupId>
            <artifactId>commons-io</artifactId>
            <version>2.18.0</version>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.1</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.codehaus.mojo</groupId>
                <artifactId>exec-maven-plugin</artifactId>
                <version>3.5.0</version>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-jar-plugin</artifactId>
                <version>3.1.0</version>
                <configuration>
                    <archive>
                        <manifestEntries>
                            <Main-Class>com.example.App</Main-Class>
                        </manifestEntries>
                    </archive>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

---

## 4. Replace `App.java` with the Example Code

Navigate to `src/main/java/com/example/` and create a file named `App.java` with the following content:

```java
package com.example;

import org.apache.commons.io.FileUtils;
import java.io.File;
import java.io.IOException;
import com.google.common.collect.ImmutableList;

public class App {
    public static void main(String[] args) {
        ImmutableList<String> fruits = ImmutableList.of("Apple", "Banana", "Cherry");
        System.out.println(fruits);

        // Define source and destination files
        File sourceFile = new File("source.txt");
        File destFile = new File("destination.txt");
        try {
            // Copy file using Apache Commons IO
            FileUtils.copyFile(sourceFile, destFile);
            System.out.println("File copied successfully!");
        } catch (IOException e) {
            System.err.println("Error occurred while copying file: " + e.getMessage());
        }
    }
}
```

---

## 5. Create the Input File

```bash
echo "This is a file created using common io dependency" > source.txt
```

---

## 6. Build the Project

```bash
mvn clean install
```

---

## 7. Run the Application

**Using Maven Exec Plugin (Recommended):**

```bash
mvn exec:java -Dexec.mainClass="com.example.App"
```

**Expected Output:**

```
[Apple, Banana, Cherry]
File copied successfully!
