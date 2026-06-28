# 🔧 Jenkins End-to-End CI/CD Pipeline

## 📌 Project Overview
An automated CI/CD pipeline using Jenkins that takes code from Git all the way to deployment on Tomcat — with zero manual steps.

## 🛠️ Tools & Technologies
| Tool | Purpose |
|------|---------|
| Jenkins | CI/CD Automation Server |
| Git | Source Code Management |
| Maven | Build Automation |
| SonarQube | Code Quality Analysis |
| Nexus | Artifact Repository |
| Tomcat | Application Deployment Server |

## 🔄 Pipeline Flow
```
Developer pushes code
        ↓
   Git Checkout
        ↓
  Maven Build (.war)
        ↓
   Unit Tests (JUnit)
        ↓
SonarQube Code Analysis
        ↓
  Quality Gate Check
        ↓
 Upload to Nexus Repo
        ↓
  Deploy to Tomcat
        ↓
Email Notification (Pass/Fail)
```

## 📁 Project Structure
```
jenkins-cicd-pipeline/
├── Jenkinsfile                          # Pipeline definition
├── pom.xml                              # Maven build config
├── src/
│   └── main/
│       └── java/com/myapp/
│           └── HelloServlet.java        # Sample Java servlet
└── README.md
```

## ⚙️ Setup Instructions

### Step 1 - Install Jenkins
```bash
sudo apt update
sudo apt install openjdk-17-jdk -y
wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt update
sudo apt install jenkins -y
sudo systemctl start jenkins
```

### Step 2 - Install Jenkins Plugins
Go to: Jenkins → Manage Jenkins → Plugins → Install:
- Maven Integration
- SonarQube Scanner
- Nexus Artifact Uploader
- Deploy to Container
- Email Extension

### Step 3 - Configure Tools in Jenkins
- Go to: Manage Jenkins → Global Tool Configuration
- Add Maven (name: Maven-3.9.0)
- Add JDK (name: JDK-17)

### Step 4 - Add Credentials in Jenkins
- Manage Jenkins → Credentials → Add:
  - `sonar-token` → SonarQube token
  - `nexus-credentials` → Nexus username/password
  - `tomcat-credentials` → Tomcat username/password

### Step 5 - Create Pipeline Job
1. New Item → Pipeline
2. Pipeline → Pipeline script from SCM
3. SCM → Git → Add your repo URL
4. Script Path → `Jenkinsfile`
5. Save → Build Now

## ✅ What Gets Automated
- ✅ Code is automatically pulled from Git
- ✅ Maven compiles and packages the app
- ✅ Unit tests run automatically
- ✅ SonarQube checks for bugs and code smells
- ✅ Artifact stored in Nexus for version management
- ✅ App deployed to Tomcat automatically
- ✅ Email sent on success or failure

## 📧 Email Notification Sample
- **Subject:** ✅ Build #5 - SUCCESS
- **Body:** Build and deployment was successful! Check: http://jenkins-url/job/...
