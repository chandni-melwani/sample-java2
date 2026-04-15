Your notes are mostly correct, but they contain repetitions and a few syntax mistakes that could cost you marks in the lab. Below is a clean, error-free, exam-ready version of the complete workflow. Follow this exactly.

---

# ✅ Jenkins CI Pipeline Using Git and Maven – Final Lab Guide

## 🔹 Step 1: Navigate to the Project Directory

```bash
cd "C:\Users\Other User\Documents\AI\sample-java2"
dir
```

This confirms you are in the correct folder.

---

## 🔹 Step 2: Create a Maven Project

### ✔ Method 1: Using Maven Archetype (Preferred)

```bash
mvn archetype:generate ^
-DgroupId=com.example ^
-DartifactId=sample-java2 ^
-DarchetypeArtifactId=maven-archetype-quickstart ^
-DinteractiveMode=false
```

If successful, Maven will display:

```
BUILD SUCCESS
```

Navigate to the generated project:

```bash
cd sample-java2
```

Verify the build:

```bash
mvn clean test
```

Expected output:

```
BUILD SUCCESS
```

---

### ✔ Method 2: Manual Setup (If Archetype Is Not Allowed)

Create directories:

```bash
mkdir src\main\java\com\example
mkdir src\test\java\com\example
type nul > pom.xml
```

> ⚠️ Correction: The command is `mkdir`, not `mkdir-p` on Windows.

---

## 🔹 Step 3: Add Source Files

### 📌 App.java

**Path:** `src/main/java/com/example/App.java`

```java
package com.example;

public class App {
    public int add(int a, int b) {
        return a + b;
    }
}
```

### 📌 AppTest.java

**Path:** `src/test/java/com/example/AppTest.java`

```java
package com.example;

import org.junit.Test;
import static org.junit.Assert.*;

public class AppTest {

    @Test
    public void testAdd() {
        App app = new App();
        assertEquals(5, app.add(2, 3));
    }
}
```

---

## 🔹 Step 4: Create `pom.xml`

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
         https://maven.apache.org/xsd/maven-4.0.0.xsd">

    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>sample-java2</artifactId>
    <version>1.0-SNAPSHOT</version>

    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13.2</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>
```

---

## 🔹 Step 5: Test the Project Locally

```bash
mvn clean test
```

Expected output:

```
BUILD SUCCESS
```

---

## 🔹 Step 6: Initialize Git Repository

```bash
git init
git add .
git commit -m "Initial Maven project with JUnit test"
```

> ⚠️ Correction: Ensure there is a space after `commit`.

---

## 🔹 Step 7: Push the Project to GitHub

```bash
git branch -M main
git remote add origin https://github.com/chandni-melwani/sample-java2.git
git push -u origin main
```

---

## 🔹 Step 8: Configure Maven in Jenkins

Verify Maven:

```bash
mvn -version
```

Your configuration:

* **Maven Version:** 3.9.9
* **MAVEN_HOME:** `C:\Program Files\Maven\apache-maven-3.9.9`
* **Java Version:** 17

In Jenkins ([http://localhost:9090](http://localhost:9090)):

1. Go to **Manage Jenkins → Tools**.
2. Scroll to **Maven Installations**.
3. Configure:

   * **Name:** `M3`
   * **Install Automatically:** Unchecked
   * **MAVEN_HOME:**

     ```
     C:\Program Files\Maven\apache-maven-3.9.9
     ```
4. Click **Save**.

---

## 🔹 Step 9: Create a Jenkins Pipeline

1. Click **New Item**.
2. Name: `sample-java2-pipeline`.
3. Select **Pipeline** → Click **OK**.
4. Paste the following script:

```groovy
pipeline {
    agent any

    tools {
        maven 'M3'
    }

    stages {
        stage('Checkout Git') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/chandni-melwani/sample-java2.git'
            }
        }

        stage('Build and Test') {
            steps {
                bat 'mvn clean test'
            }
        }
    }
}
```

Click **Save**.

---

## 🔹 Step 10: Run the Jenkins Pipeline

1. Click **Build Now**.
2. Open **Console Output**.

### ✅ Expected Output

```
BUILD SUCCESS
Finished: SUCCESS
```

---

## 🔄 Complete Workflow

```
Developer → GitHub → Jenkins → Maven → JUnit → Build Success
```

---

## 🎤 Viva-Ready Answer

“In this experiment, I created a Maven-based Java project and added a JUnit test case. After verifying the build locally using Maven, I pushed the project to GitHub. I configured Maven in Jenkins and created a declarative pipeline. Jenkins automatically checked out the code, built the project, and executed the tests, demonstrating a Continuous Integration pipeline.”

---

## ⚠️ Common Mistakes to Avoid

| Mistake                       | Correction                      |
| ----------------------------- | ------------------------------- |
| `mkdir-p` on Windows          | Use `mkdir`                     |
| `git commit-m`                | Use `git commit -m`             |
| Missing quotes in `cd` path   | Use `" "` for paths with spaces |
| Named parameters in Java      | Use `app.add(2, 3)`             |
| Wrong Maven path in Jenkins   | Use the exact `MAVEN_HOME`      |
| Nested `sample-java2` folders | Work inside the inner folder    |

---

## ✅ Final Exam Checklist

| Task                        | Status |
| --------------------------- | ------ |
| Maven Project Created       | ⬜      |
| Code Compiles Successfully  | ⬜      |
| `mvn clean test` Successful | ⬜      |
| Project Pushed to GitHub    | ⬜      |
| Maven Configured in Jenkins | ⬜      |
| Pipeline Created            | ⬜      |
| Jenkins Build Successful    | ⬜      |

**Confidence Level: 100%**
You are fully prepared for your lab exam. If you'd like, share your Jenkins console output and I’ll verify it before submission. 🚀
