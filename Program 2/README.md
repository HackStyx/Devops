# Maven Selenium Project Setup with ChromeDriver

## 1. Install Java (if not already installed)

```bash
sudo apt update 
sudo apt install openjdk-21-jdk 
java -version
```

---

## 2. Install Maven

```bash
sudo apt install maven
mvn -version
```

---

## 3. Verify Google Chrome Installation

```bash
google-chrome --version
```

---

## 4. Download and Install ChromeDriver

1. **Install JQ (JSON processor):**

```bash
sudo apt install jq
```

2. **Get Chrome Version:**

```bash
CHROME_VERSION=$(google-chrome --version | awk '{print $3}' | cut -d'.' -f1-3)
```

3. **Get Latest ChromeDriver Version:**

```bash
LATEST_DRIVER=$(curl -s "https://googlechromelabs.github.io/chrome-for-testing/latest-patch-versions-per-build.json" | jq -r ".builds["$CHROME_VERSION"].version")
```

4. **Download and Install ChromeDriver:**

```bash
wget https://storage.googleapis.com/chrome-for-testing-public/$LATEST_DRIVER/linux64/chromedriver-linux64.zip
unzip chromedriver-linux64.zip
sudo mv chromedriver-linux64/chromedriver /usr/local/bin/chromedriver
sudo chmod +x /usr/local/bin/chromedriver
```

5. **Verify ChromeDriver Installation:**

```bash
chromedriver --version
```

---

## 5. Create Maven Project

```bash
mvn archetype:generate -DgroupId=com.example -DartifactId=MyMavenSeleniumApp01 -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
cd MyMavenSeleniumApp01
```

---

## 6. Update `pom.xml` File

Replace the content of the `pom.xml` file with the following:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                             http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>MyMavenSeleniumApp01</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>jar</packaging>
    <name>MyMavenSeleniumApp01</name>

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
            <groupId>org.seleniumhq.selenium</groupId>
            <artifactId>selenium-java</artifactId>
            <version>4.29.0</version>
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
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>3.3.0</version>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>shade</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>
```

---

## 7. Create `App.java` File

Navigate to `src/main/java/com/example/` and create a file named `App.java` with the following content:

```java
package com.example;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

public class App {
    public static void main(String[] args) {
        WebDriver driver = new ChromeDriver();
        driver.get("https://www.saucedemo.com/");
        driver.manage().window().maximize();
        driver.findElement(By.id("user-name")).sendKeys("standard_user");
        driver.findElement(By.id("password")).sendKeys("secret_sauce");
        driver.findElement(By.id("login-button")).click();
    }
}
```

---

## 8. Build the Project

```bash
mvn clean package
```

---

## 9. Run the Application

**Option 1: From the JAR (After Successful Build):**

```bash
java -jar target/MyMavenSeleniumApp01-1.0-SNAPSHOT.jar
```

**Option 2: Directly with Maven:**

```bash
mvn exec:java -Dexec.mainClass="com.example.App"
```

---

## 10. (Optional) Cleanup:

```bash
rm chromedriver-linux64.zip
```

---

## 11. Troubleshooting

- Ensure ChromeDriver is correctly located in `/usr/local/bin/`.
- If JAR does not execute, try:

```bash
mvn exec:java -Dexec.mainClass="com.example.App"
