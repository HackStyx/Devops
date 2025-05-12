## Prerequisites
- Java Development Kit (JDK) installed (`java --version`)
- Apache Maven installed (`mvn --version`)
- Gradle installed (`gradle --version`)
- Ansible installed (`ansible --version`)

## Maven Project Structure
```
First_Maven_App/
│── pom.xml
│── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/
│   │   │       └── example/
│   │   │           └── App.java
│   ├── test/
│   │   ├── java/
│   │   │   └── com/
│   │   │       └── example/
│   │   │           └── AppTest.java
│── target/
│   ├── First_Maven_App-1.0-SNAPSHOT.jar
│   ├── classes/
│   │   └── com/example/App.class
│   ├── test-classes/
│   │   └── com/example/AppTest.class
```

### Steps to Create and Build a Maven Project

#### 1. Generate a Maven Project
```bash
mvn archetype:generate -DgroupId=com.example -DartifactId=First_Maven_App -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

#### 2. Navigate to the Project Directory
```bash
cd First_Maven_App
```

#### 3. Modify `pom.xml` to Include Build and Execution Configurations
Update the `pom.xml` file with the following configuration:
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.example</groupId>
  <artifactId>First_Maven_App</artifactId>
  <packaging>jar</packaging>
  <version>1.0-SNAPSHOT</version>
  <name>First_Maven_App</name>
  <url>http://maven.apache.org</url>

  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>3.8.1</version>
      <scope>test</scope>
    </dependency>
  </dependencies>

  <build>
    <plugins>
      <!-- Maven Compiler Plugin -->
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.8.1</version>
        <configuration>
          <source>1.8</source>
          <target>1.8</target>
        </configuration>
      </plugin>

      <!-- Maven Surefire Plugin for Running Tests -->
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-surefire-plugin</artifactId>
        <version>2.22.2</version>
      </plugin>

      <!-- Maven JAR Plugin -->
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-jar-plugin</artifactId>
        <version>3.0.1</version>
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

#### 4. Edit the Main Java File (Optional)
```bash
gedit src/main/java/com/example/App.java
```

#### 5. Build the Project
```bash
mvn clean install
```

#### 6. Package the Project
```bash
mvn package
```

#### 7. Run the Tests
```bash
mvn test
```

### Steps to Run the Maven Application

#### 1. Ensure the Project is Built
```bash
mvn clean install
```

#### 2. Navigate to the Target Directory
```bash
cd target
```

#### 3. Run the JAR File
```bash
java -jar First_Maven_App-1.0-SNAPSHOT.jar
```
*(Replace `First_Maven_App-1.0-SNAPSHOT.jar` with the actual JAR file name if different.)*

#### 4. Run the Main Class Directly
```bash
mvn exec:java -Dexec.mainClass="com.example.App"
```
*(Ensure `exec-maven-plugin` is configured in `pom.xml` for this to work.)*
