# 🚀 Secure Jenkins CI/CD Automation using Shared Library

A production-style Jenkins CI/CD pipeline that automates application delivery using **Jenkins Shared Libraries**, **Docker Compose**, **DevSecOps security scanning**, **email notifications**, and **Jenkins Agents**.

This project demonstrates how to build a reusable and secure CI/CD pipeline by separating pipeline logic into a Jenkins Shared Library while integrating multiple security tools for code, dependency, container, and runtime scanning.

---

# 📌 Features

- Jenkins Declarative Pipeline
- Jenkins Shared Library
- Jenkins Controller & Agent Architecture
- Docker Compose Build & Deployment
- Docker Hub Integration
- Automated Email Notifications
- SonarQube Code Quality Analysis
- GitLeaks Secret Detection
- Semgrep SAST Scanning
- OWASP Dependency Check
- Trivy Filesystem Scan
- OWASP ZAP DAST Scan
- Scan Report Generation
- Report Email Attachments
- Fully Automated CI/CD Workflow

---

# 🏗️ Architecture

```
Developer
    │
    ▼
GitHub Repository
    │
    ▼
Webhook / Build Trigger
    │
    ▼
Jenkins Controller
    │
    ▼
Jenkins Agent
    │
    ▼
Shared Library
    │
    ▼
Git Clone
    │
    ▼
GitLeaks
    │
    ▼
Semgrep
    │
    ▼
SonarQube
    │
    ▼
OWASP Dependency Check
    │
    ▼
Docker Compose Build
    │
    ▼
Trivy Scan
    │
    ▼
Docker Hub Push
    │
    ▼
Docker Deployment
    │
    ▼
OWASP ZAP
    │
    ▼
Email Notification
```

---

# 📂 Repository Structure

```
Secure-Jenkins-CICD-Automate
│
├── backend
├── frontend
├── database
├── docker-compose.yml
├── Jenkinsfile
├── README.md
└── ...
```

---

# 🔐 Jenkins Shared Library

Pipeline logic is separated into a reusable Jenkins Shared Library.

```
jenkins-shared-library
│
├── vars
│   ├── clone.groovy
│   ├── dockerDeploy.groovy
│   ├── dockerRegistry.groovy
│   ├── gitleaks.groovy
│   ├── notify.groovy
│   ├── owasp.groovy
│   ├── owaspZap.groovy
│   ├── semgrep.groovy
│   ├── sonarcube.groovy
│   └── trivy.groovy
│
└── README.md
```

Using a Shared Library keeps Jenkinsfiles clean and promotes reusable pipeline code across multiple projects.

---

# 📦 Pipeline Workflow

The pipeline performs the following tasks automatically:

1. Clone Repository
2. GitLeaks Secret Scan
3. Semgrep Static Analysis
4. SonarQube Code Analysis
5. OWASP Dependency Check
6. Docker Compose Build
7. Trivy Filesystem Scan
8. Docker Hub Login
9. Docker Image Push
10. Docker Logout
11. Deploy Containers
12. OWASP ZAP Dynamic Scan
13. Email Notification with Reports

---

# 🔒 Why Security Tools?

This project integrates multiple security layers throughout the CI/CD pipeline.

| Tool | Purpose |
|------|---------|
| GitLeaks | Detects hardcoded secrets, API keys, and passwords |
| Semgrep | Static Application Security Testing (SAST) |
| SonarQube | Code quality, bugs, vulnerabilities, and code smells |
| OWASP Dependency Check | Detects vulnerable third-party libraries |
| Trivy | Container and filesystem vulnerability scanning |
| OWASP ZAP | Dynamic Application Security Testing (DAST) |

This layered approach helps identify security issues before software reaches production.

---

# 📧 Email Notification

The pipeline sends automated email notifications after every build.

Notifications include:

- Build Status
- Build Number
- Job Name
- Build URL
- Attached Security Reports

Example attachments:

- Trivy Report
- GitLeaks Report
- Semgrep Report
- Dependency Check Report
- ZAP Report

---

# 📨 Gmail SMTP Configuration

To enable Jenkins email notifications:

### 1. Enable Two-Factor Authentication

Enable 2-Step Verification on your Gmail account.

### 2. Generate an App Password

Google Account

```
Security  ⟶  App Passwords  ⟶  Mail  ⟶  Generate
```

Use the generated App Password instead of your Gmail password.

---

### Jenkins Configuration

```
Manage Jenkins   ⟶   Configure System
```

Configure:

```
SMTP Server ⟶ smtp.gmail.com  ⟶  Port  ⟶ 587  ⟶ Authentication  ⟶  Enabled  ⟶  TLS  ⟶  Enabled  ⟶  SSL  ⟶  Disabled
```

Add your Gmail credentials using the generated App Password.

---

# 🤖 Jenkins Agent Configuration

The pipeline executes on a Jenkins Agent instead of the Controller.

Using agents provides several benefits:

- Prevents heavy builds from consuming Controller resources
- Isolates Docker workloads
- Improves Jenkins stability
- Supports distributed builds
- Enables parallel execution

Example:

```
Controller  ⟶  SSH Agent  ⟶  Docker Build  ⟶  Deployment
```

Pipeline Example:

```groovy
agent {
    label 'dev-agent-key'
}
```

---

# 📚 Configure Jenkins Shared Library

Go to:

```
Manage Jenkins  ⟶  System  ⟶  Global Trusted Pipeline Libraries
```

Configure:

| Setting | Value |
|----------|-------|
| Name | shared |
| Default Version | main |
| Retrieval | Modern SCM |
| Repository | Your Shared Library Git Repository |

---

# 📜 Using the Shared Library

Import the library:

```groovy
@Library('shared') _
```

Example:

```groovy
stage('GitLeaks') {
    steps {
        script {
            gitleaks()
        }
    }
}
```

The Jenkinsfile only orchestrates stages, while the implementation resides in the Shared Library.

---

# 📊 Generated Reports

The pipeline generates reports including:

```
reports/

├── gitleaks-report.json
├── semgrep-report.json
├── trivy-report.json
├── dependency-check-report.html
├── dependency-check-report.json
└── zap-report.json
```

These reports can be archived and sent as email attachments.

---

# 🛠️ Technologies Used

- Jenkins
- Jenkins Shared Library
- Docker
- Docker Compose
- GitHub
- SonarQube
- Trivy
- Semgrep
- GitLeaks
- OWASP Dependency Check
- OWASP ZAP
- Gmail SMTP
- Linux
- SSH
- Groovy
- Declarative Pipeline

---

# 🚀 Future Improvements

- Kubernetes Deployment
- Helm Charts
- ArgoCD GitOps
- AWS ECR Integration
- Amazon ECS Deployment
- Amazon EKS Deployment
- Slack Notifications
- Microsoft Teams Notifications
- HashiCorp Vault Integration
- Terraform Infrastructure Provisioning

---

# 📖 Learning Objectives

This project demonstrates:

- Jenkins Administration
- Shared Library Development
- Secure CI/CD Design
- DevSecOps Integration
- Docker Automation
- Pipeline Reusability
- Distributed Jenkins Architecture
- Automated Security Scanning
- Enterprise CI/CD Best Practices

---

# 👨‍💻 Author

**Ahsan Mustafa**

DevOps | Cloud | Linux | AWS | Docker | Jenkins | DevSecOps

---
