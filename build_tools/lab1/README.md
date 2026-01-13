# Ivolve Application - Build and Run Guide

This project demonstrates the lifecycle of the Ivolve application, from environment setup to final verification using **Gradle**.

---

## 📋 Steps to Build and Run

### 1. Install Gradle

Ensure **Gradle** and **Java** are installed on your system.

* Check Gradle:

```bash
gradle -v
```

* Check Java:

```bash
java -version
```

---

### 2. Clone Source Code

Download the project repository to your local environment:

```bash
git clone https://github.com/Ibrahim-Adel15/build1.git
cd build1
```

---

### 3. Run Unit Tests

Execute the testing suite to ensure code integrity:

```bash
gradle test
```

---

### 4. Build the Application

Compile the project and generate the executable artifact:

```bash
gradle build
```

The artifact is generated at:

```
build/libs/ivolve-app.jar
```

---

### 5. Run the Application

Start the application using the Java Runtime Environment:

```bash
java -jar build/libs/ivolve-app.jar
```

---

### 6. Verify App is Working

Check the terminal logs to ensure the application has started successfully and is listening for requests.

---

## 🛠 Summary Table

| Step | Action            | Command                                                  |
| ---- | ----------------- | -------------------------------------------------------- |
| 1    | Clone Repository  | `git clone https://github.com/Ibrahim-Adel15/build1.git` |
| 2    | Run Unit Tests    | `gradle test`                                            |
| 3    | Build Application | `gradle build`                                           |
| 4    | Run Application   | `java -jar build/libs/ivolve-app.jar`                    |

---

