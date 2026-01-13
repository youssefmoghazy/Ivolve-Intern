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
![Gradle Test](https://private-user-images.githubusercontent.com/115780537/535237820-b70459fc-87a3-4511-b317-6546135623c4.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NjgzMjc5NDQsIm5iZiI6MTc2ODMyNzY0NCwicGF0aCI6Ii8xMTU3ODA1MzcvNTM1MjM3ODIwLWI3MDQ1OWZjLTg3YTMtNDUxMS1iMzE3LTY1NDYxMzU2MjNjNC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjYwMTEzJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI2MDExM1QxODA3MjRaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT03ODI0NDkxMDY4MGVmOWZmZGUyZDNhMWM2ZDg4YmU2YWI1YWQxNDVjNTk5OTI3NTAzNTVjM2I3MWEyODVhZGFkJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.EryGEqjVpzHF223EohZLHuF3h7g84g-CF2xN1v5gq_A)
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

