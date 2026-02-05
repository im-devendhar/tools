
---

## 🔍 SonarQube Integration Steps (Code Quality Analysis)

This project uses **SonarQube** to perform **static code analysis** and ensure code quality as part of the CI/CD pipeline.

---

### 1️⃣ Install SonarQube

SonarQube was installed and run on the server (EC2) and made accessible on port **9000**.

```bash
http://<SERVER-IP>:9000
```

Default login:

```
Username: admin
Password: admin
```

(Change password on first login)

---

### 2️⃣ Generate SonarQube Authentication Token

To allow Jenkins to communicate securely with SonarQube:

1. Login to SonarQube
2. Go to:

   ```
   Profile → My Account → Security
   ```
3. Generate a **User Token**

   * Name: `jenkins-sonar-token`
   * Type: User Token
4. Copy the token (shown only once)

---

### 3️⃣ Add SonarQube Token to Jenkins

In Jenkins:

```
Manage Jenkins → Credentials → Global → Add Credentials
```

* Kind: **Secret Text**
* Secret: *(Paste SonarQube token)*
* ID: `sonar-token`
* Description: SonarQube token for Jenkins

---

### 4️⃣ Configure SonarQube Server in Jenkins

In Jenkins:

```
Manage Jenkins → System → SonarQube installations
```

Fill the details:

* Name: `sonarqube`
* Server URL:

  ```
  http://<SERVER-IP>:9000
  ```
* Server authentication token: `sonar-token`

Save the configuration.

---

### 5️⃣ Install SonarQube Scanner in Jenkins

In Jenkins:

```
Manage Jenkins → Global Tool Configuration
```

Under **SonarQube Scanner**:

* Name: `SonarScanner`
* Enable **Install automatically**
* Save

---

### 6️⃣ Configure Project for SonarQube Analysis

Add a `sonar-project.properties` file in the GitHub repository:

```properties
sonar.projectKey=demo-project
sonar.projectName=Demo Project
sonar.sources=.
```

---

### 7️⃣ Run SonarQube Analysis from Jenkins Pipeline

SonarQube analysis is triggered from Jenkins using the following pipeline stage:

```groovy
stage('SonarQube Analysis') {
  steps {
    withSonarQubeEnv('sonarqube') {
      sh 'sonar-scanner'
    }
  }
}
```

---

### 8️⃣ Verify Analysis Results

* Jenkins console shows **ANALYSIS SUCCESSFUL**
* Project appears in SonarQube dashboard
* Code issues, bugs, vulnerabilities, and quality gate status are visible

---

## ✅ Outcome

* Automated static code analysis
* Improved code quality and maintainability
* Integrated seamlessly into CI/CD pipeline

---

## 🎯 One-Line Explanation (for Viva / Interview)

> SonarQube is integrated with Jenkins to automatically analyze source code during pipeline execution and enforce code quality standards.

---

