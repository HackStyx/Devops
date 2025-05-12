## **1. Install Apache Tomcat**

1. Restart the Ubuntu virtual box and press **Shift + Esc** while booting.
2. Restart again and press **Shift** key when the black screen appears.
3. Enter the root directory:

    ```bash
    sudo -i
    ```

4. Update and upgrade packages:

    ```bash
    sudo apt update && sudo apt upgrade -y
    ```

5. Navigate to the `/tmp` directory:

    ```bash
    cd /tmp
    ```

6. Download Apache Tomcat:

    ```bash
    wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.100/bin/apache-tomcat-9.0.100.tar.gz
    ```

7. Create the tomcat directory:

    ```bash
    cd /opt
    sudo mkdir tomcat
    ```

8. Extract the downloaded tar file into `/opt/tomcat`:

    ```bash
    sudo tar -xvzf /tmp/apache-tomcat-9.0.100.tar.gz -C /opt/tomcat --strip-components=1
    ```

9. Navigate to the Tomcat configuration folder:

    ```bash
    cd /opt/tomcat/conf
    ```

10. Open `server.xml` to change the default port (8080 to 9090):

    ```bash
    sudo gedit server.xml
    ```

    - Locate the `<Connector port="8080" ...>` and change it to:

    ```xml
    <Connector port="9090" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" />
    ```

11. Add a user in `tomcat-users.xml`:

    ```bash
    sudo gedit tomcat-users.xml
    ```

    - Add the following user:

    ```xml
    <user username="admin" password="Admin" roles="manager-gui"/>
    ```

12. Start Tomcat:

    ```bash
    cd /opt/tomcat/bin
    sh startup.sh
    ```

13. Access Tomcat in the browser:

    - Open: `localhost:9090`

---

##  **2. Create a New Maven Web Application**

1. Generate the Maven project:

    ```bash
    mvn archetype:generate -DgroupId=com.example -DartifactId=MyMavenWebApp01 -DarchetypeArtifactId=maven-archetype-webapp -DinteractiveMode=false
    ```

2. Navigate to the project directory:

    ```bash
    cd MyMavenWebApp01
    ```

---

## **3. Update `pom.xml` with Servlet API and WAR Plugin**

Replace the `pom.xml` content with the following:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>MyMavenWebApp01</artifactId>
  <packaging>war</packaging>
  <version>1.0-SNAPSHOT</version>
  <name>MyMavenWebApp01</name>

  <dependencies>
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>javax.servlet-api</artifactId>
      <version>4.0.1</version>
      <scope>provided</scope>
    </dependency>
  </dependencies>

  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-war-plugin</artifactId>
        <version>3.4.0</version>
      </plugin>
    </plugins>
    <finalName>MyMavenWebApp01</finalName>
  </build>
</project>
```

---

## **4. Verify Project Structure**

Run the command:

```bash
tree
```

- Project structure should look like this:

```
── pom.xml
├── src
│   └── main
│       ├── resources
│       └── webapp
│           ├── index.jsp
│           └── WEB-INF
│               └── web.xml
```

---

## **5. Customize `index.jsp`**

Open `src/main/webapp/index.jsp` and modify the content:

```html
<html>
<body>
<h2>Hello, Maven Web Application!</h2>
</body>
</html>
```

---

## **6. Build the Project**

```bash
mvn clean install
```

- The WAR file will be generated in the `target` directory:

```
target
├── MyMavenWebApp01.war
```

---

## **7. Deploy the WAR File to Tomcat**

1. Copy the WAR file to Tomcat's `webapps` folder:

    ```bash
    sudo cp target/MyMavenWebApp01.war /opt/tomcat/webapps
    ```

2. Restart Tomcat:

    ```bash
    cd /opt/tomcat/bin
    sh shutdown.sh
    sh startup.sh
    ```

3. Open the browser and go to:

    - `localhost:9090/MyMavenWebApp01`

    - The `Hello, Maven Web Application!` message should be displayed.

---

##  **8. Troubleshooting and Cleanup**

- Verify port configuration in `server.xml`.
- Ensure the WAR file is correctly placed in the `webapps` folder.
- Check the Tomcat logs for error messages:

    ```bash
    tail -f /opt/tomcat/logs/catalina.out
    ```

- Stop Tomcat using:

    ```bash
    sh shutdown.sh
    
