🚀 Project Title : 3-Tier Web Application Deployment using Jenkins CI/CD, Docker, SonarQube & DevSecOps Practices.

📌 Project Overview : This project demonstrates the deployment of a production-style 3-tier web application using DevOps and DevSecOps practices. The application architecture consists of:

**Frontend Layer** – User Interface
**Backend Layer** – Application/API services
**Database Layer** – MySQL database

<img width="1080" height="720" alt="Architecture Diagram" src="https://github.com/user-attachments/assets/b013acb7-42d8-4ce1-96ee-260978eafa8a" />
The project focuses on automating the complete CI/CD workflow using Jenkins, containerization using Docker, code quality analysis using SonarQube, and vulnerability scanning using Trivy.

The deployment was performed on an AWS EC2 Ubuntu server with Dockerized services and automated Jenkins pipelines.

# ⭐ STAR Method Explanation

## 🟢 Situation
Modern applications require automated deployment pipelines, secure containerized environments, code quality validation, and vulnerability scanning before deployment to production environments. Manual deployment processes are time-consuming, error-prone, and difficult to scale.
## 🟢 Task
The task was to build and deploy a complete 3-tier application infrastructure using DevOps and DevSecOps tools that can:
* Automate application deployment
* Perform continuous integration and delivery
* Scan source code quality
* Detect container vulnerabilities
* Deploy application containers efficiently
* Maintain secure and reliable deployments
--
## 🟢 Action
Implemented the following:
* Provisioned AWS EC2 Ubuntu server infrastructure
* Installed and configured Jenkins CI/CD server
* Installed Docker and Docker Compose
* Configured SonarQube for static code analysis
* Installed Trivy for vulnerability scanning
* Created Jenkins pipelines for automated deployment
* Configured DockerHub authentication
* Implemented SonarQube webhook integration with Jenkins
* Containerized frontend, backend, and database services
* Deployed the application using Docker containers
* Validated database connectivity and application functionality
---
## 🟢 Result
Successfully achieved:
* Automated CI/CD deployment pipeline
* Dockerized 3-tier architecture deployment
* Automated code quality checks using SonarQube
* Container image vulnerability scanning using Trivy
* Faster and repeatable deployment process
* Improved application security and deployment reliability
* Real-time deployment and monitoring workflow
---

# 🛠️ Tools & Technologies Used
| Tool                  | Purpose                    | Significance                                       |
| --------------------- | -------------------------- | -------------------------------------------------- |
| Jenkins               | CI/CD Automation           | Automates build, testing, and deployment workflows |
| Docker                | Containerization           | Packages applications into portable containers     |
| SonarQube             | Code Quality Analysis      | Detects bugs, vulnerabilities, and code smells     |
| Trivy                 | Vulnerability Scanner      | Scans Docker images for security vulnerabilities   |
| AWS EC2               | Cloud Infrastructure       | Hosts the deployment environment                   |
| MySQL                 | Database                   | Stores application data                            |
| Git & GitHub          | Version Control            | Source code management and collaboration           |
| Docker Compose        | Multi-container Management | Manages multiple application containers            |
| Linux Shell Scripting | Automation                 | Simplifies repetitive operational tasks            |

---
# 🔐 Ports Used
| Port | Service     |
| ---- | ----------- |
| 8080 | Jenkins     |
| 9000 | SonarQube   |
| 5000 | Application |
| 3000 | Database    |

---
# ⚙️ Step-by-Step Project Execution
# 1️⃣ Launch AWS EC2 Instance
* Create Ubuntu EC2 instance
* Instance Type: t2 large
* Storage: 30 GB
* Create & download Key Pair
* Allow inbound ports:
8080,9000,5000,3000
---
☁️ AWS EC2 Configuration
Component	Details
Cloud Provider	AWS
EC2 Type	t2.large
Storage	50 GB
OS	Ubuntu
AMI ID	ami-05d2d839d4f73aafb
Authentication	SSH Key Pair
# 2️⃣ Connect to EC2 via SSH
ssh -i <key.pem> ubuntu@<Public-IP>

Switch to root user:
sudo -i
# 3️⃣ Clone GitHub Repository
git clone https://github.com/chetanccd318/chetanccd318-3-tier-Application-Deployment-DevSecOps.git

# 4️⃣ Install Java & Jenkins
sudo apt update
sudo apt install fontconfig openjdk-21-jre -y
java -version

Install Jenkins:
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
https://pkg.jenkins.io/debian/jenkins.io-2023.key

echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
https://pkg.jenkins.io/debian binary/ | sudo tee \
/etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt update
sudo apt install jenkins -y
Access Jenkins:
http://<Public-IP>:8080
Get Jenkins password:
cat /var/lib/jenkins/secrets/initialAdminPassword

# 5️⃣ Install Docker
Move to project directory:
cd 3tierapplicationdeplyDevSecOps
Give executable permission:
chmod +x *.sh
Run Docker installation script:
./2nd-Docker.sh

# 6️⃣ Configure Jenkins Permissions
sudo usermod -aG docker jenkins
sudo systemctl restart jenkins
sudo -u jenkins docker ps

# 7️⃣ Install Python & Docker Compose
sudo apt-get update
sudo apt-get install -y python3-venv python3-pip
sudo apt-get install -y docker-compose-plugin

Or run:
./3rd-Adduser+python.sh
---
# 8️⃣ Install Trivy

curl -sfL https://raw.githubusercontent.com/aquasecurity/trivy/main/contrib/install.sh | sudo sh -s -- -b /usr/local/bin v0.70.0
Verify:
trivy --version
-
# 9️⃣ Install & Run SonarQube
docker run -d --name sonar -p 9000:9000 sonarqube:lts-community
Verify:
docker ps
``
Access:
http://<Public-IP>:9000

Default credentials:
Username: admin
Password: admin
``
 🔟 Jenkins Plugin Installation
Install plugins:
* SonarQube Scanner
* Docker
* Docker Commons
* Docker Pipeline
* Docker API
* docker-build-step
* Pipeline Stage View

Restart Jenkins after installation.
---
# 1️⃣1️⃣ Configure SonarQube in Jenkins
## Create SonarQube Token

Go to: SonarQube → Administration → Security → Users → Tokens
Generate token.
--
## Add Token in Jenkins- Manage Jenkins → Credentials → Global → Add Credentials
`
Secret Text
ID:
sonar-token
``
# 1️⃣2️⃣ Configure SonarQube Webhook

Go to: SonarQube → Administration → Configuration → Webhooks
`
Webhook URL:
http://<Jenkins-IP>:8080/sonarqube-webhook/
``
# 1️⃣3️⃣ Configure SonarQube Server in Jenkins

Manage Jenkins → System → SonarQube Servers
``
Add:
* Name: sonar
* Server URL: `http://<Public-IP>:9000`
* Token: sonar-token
---

# 1️⃣4️⃣ Configure DockerHub Credentials : Manage Jenkins → Credentials → Global
``
Add:
* Username
* Password
* ID: docker
---
# 1️⃣5️⃣ Create Jenkins Pipeline Job

* Create New Pipeline Job
* Copy Jenkins pipeline from repository
* Update Docker image username
* Build Pipeline
---
# 1️⃣6️⃣ Access Application

http://<Public-IP>:5000
``
# 🗄️ Database Verification
Connect MySQL container:
docker exec -it mysql_db mysql -u root -p
``
Database commands:
USE devops_exam;
SHOW TABLES;
DESCRIBE results;
SELECT * FROM results;
SELECT * FROM results ORDER BY score DESC;
SELECT AVG(score) FROM results;
SELECT COUNT(*) FROM results;
``
# 🔎 Trivy Vulnerability Scanning
Scan Docker images:
trivy image nginx:latest
``
Scan MySQL image:
trivy image mysql:5.7
```
# 📊 Key DevOps & DevSecOps Features

✅ CI/CD Automation using Jenkins
✅ Dockerized Multi-Container Deployment
✅ Code Quality Analysis using SonarQube
✅ Container Vulnerability Scanning using Trivy
✅ Automated Deployment Workflow
✅ Cloud-Based Infrastructure on AWS
✅ Real-World Production Deployment Concepts
✅ Database Validation & Monitoring
--
# 🚀 Project Outcome

This project provided hands-on experience with:

* CI/CD pipeline implementation
* Infrastructure provisioning
* Secure container deployment
* DevSecOps workflow integration
* Docker container orchestration
* Code quality management
* Vulnerability scanning
* Production deployment practices
--
# 📚 Learning Outcomes

* Learned end-to-end DevOps pipeline implementation
* Understood containerized application deployment
* Practiced DevSecOps security integration
* Gained hands-on Jenkins automation experience
* Learned SonarQube and Trivy integration
* Improved Linux troubleshooting and automation skills
--
👨‍💻 Author
Chetan Deshmukh
DevOps | Cloud | CI/CD | Docker | Kubernetes | AWS | Jenkins | Terraform







