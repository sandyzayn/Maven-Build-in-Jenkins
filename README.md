# 🚀 Jenkins + Maven Build Pipeline (Using Docker)

This guide demonstrates building a simple **Java** application using **Jenkins** and **Maven** inside a **Docker** container.

---

## 📂 Project Structure

```
hello-java-maven/
├── pom.xml
└── src/main/java/HelloWorld.java
```

- **`HelloWorld.java`** – Sample Java program  
- **`pom.xml`** – Maven configuration (Java version, artifact info, build settings)

---

## 🛠 Prerequisites

- [Docker 🐳](https://docs.docker.com/get-docker/) installed
- [Git 🌀](https://git-scm.com/downloads) installed
- 📦 GitHub repository containing the Maven project

---

## 🚦 Quick Start

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/sandyzayn/Maven-Build-in-Jenkins.git
cd Maven-Build-in-Jenkins
```

---

### 2️⃣ Run Jenkins in Docker

```bash
docker run -d \
  --name jenkins \
  -p 8080:8080 \
  -p 50000:50000 \
  -v jenkins_home:/var/jenkins_home \
  jenkins/jenkins:lts
```

---

### 3️⃣ Get Jenkins Admin Password

```bash
docker exec -it jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

🔑 Use this password to unlock Jenkins at [http://localhost:8080](http://localhost:8080)

---

### 4️⃣ Configure Maven in Jenkins

1. Go to **Manage Jenkins → Global Tool Configuration**
2. Under **Maven**, click **Add Maven**
3. Name it (e.g., `Maven-3.8.6`)
4. Select **Install automatically**

---

### 5️⃣ Create a Freestyle Job

1. **New Item → Freestyle project**
2. Enter job name: `hello-java-maven-build`
3. **Source Code Management → Git**
   - **Repository URL:**  
     ```
     https://github.com/sandyzayn/Maven-Build-in-Jenkins
     ```
   - **Branch Specifier:**  
     ```
     */main
     ```
4. **Build → Invoke top-level Maven targets**
   - **Goals:**  
     ```
     clean package
     ```
   - If `pom.xml` is inside a subfolder:  
     ```
     hello-java-maven/pom.xml
     ```

---

### 6️⃣ Build the Project

- Click **Build Now**
- On success, you’ll see:
  ```
  [INFO] BUILD SUCCESS
  ```
- Output `.jar` file will be in:
  ```
  target/
  ```

---

## 🐞 Troubleshooting

### ⚠️ Port 8080 Already in Use

```powershell
netstat -ano | findstr :8080
taskkill /PID <PID> /F
```

### 📄 No POM Found

- Ensure `pom.xml` is in the root of your repo, or set its correct path in Jenkins.

---

## 🖼️ Screenshots

<div align="center">
  <img width="900" alt="Jenkins Dashboard" src="https://github.com/user-attachments/assets/9e1db572-a210-46e9-af4a-412ec61110b7" />
  <br><br>
  <img width="900" alt="Jenkins Configure Maven" src="https://github.com/user-attachments/assets/58eb9e92-e078-4b4a-95bd-12d2d35d0b7a" />
  <br><br>
  <img width="900" alt="Add Maven Tool" src="https://github.com/user-attachments/assets/9fc93030-abea-4556-812f-77f504a50ad2" />
  <br><br>
  <img width="900" alt="Create Job" src="https://github.com/user-attachments/assets/1910b022-0d5e-42d8-9534-deb5f33c8366" />
  <br><br>
  <img width="900" alt="Job Configuration" src="https://github.com/user-attachments/assets/0af5411b-38de-4524-8239-d94c35657487" />
  <br><br>
  <img width="900" alt="Build Success" src="https://github.com/user-attachments/assets/8aaa8f57-4729-4914-841e-588391c12e3a" />
  <br><br>
  <img width="900" alt="Build Console Output" src="https://github.com/user-attachments/assets/5a5f4e39-274e-45af-942e-83c909b597d9" />
  <br><br>
  <img width="900" alt="Success" src="https://github.com/user-attachments/assets/7018367b-aa09-487c-ab5e-8cb4c74a24c8" />
</div>

---

