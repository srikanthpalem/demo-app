\# 🚀 Production-Ready CI/CD Pipeline (Jenkins + Docker + Kubernetes)



A complete, end-to-end CI/CD pipeline that automatically builds, containerizes, and deploys a Java application to Kubernetes on every GitHub push.



\---



\## 🧩 Tech Stack



\* \*\*SCM\*\*: GitHub

\* \*\*CI/CD\*\*: Jenkins (Declarative Pipeline)

\* \*\*Build\*\*: Maven, Java 17

\* \*\*Containerization\*\*: Docker

\* \*\*Registry\*\*: Docker Hub

\* \*\*Orchestration\*\*: Kubernetes (Docker Desktop)

\* \*\*Webhook Tunneling\*\*: ngrok



\---



\## 🏗️ Architecture



```text

GitHub Push → Webhook (ngrok) → Jenkins → Maven Build → Docker Build → Docker Push → Kubernetes Deploy

```



\---



\## 📁 Repository Structure



```text

/demo-app

&#x20;├── src/

&#x20;├── pom.xml

&#x20;├── Dockerfile

&#x20;├── deployment.yaml

&#x20;├── service.yaml

&#x20;├── Jenkinsfile

&#x20;└── README.md

```



\---



\## ⚙️ Prerequisites



\* Java 17

\* Maven

\* Git

\* Docker Desktop (with Kubernetes enabled)

\* kubectl

\* Jenkins (Windows service)

\* Docker Hub account

\* ngrok account



\---



\## 🔧 Setup Guide



\### 1) Jenkins Installation \& Tools



\* Install Jenkins on Windows

\* Configure tools in \*\*Manage Jenkins → Global Tool Configuration\*\*:



&#x20; \* JDK: `JDK17`

&#x20; \* Maven: `Maven`



\---



\### 2) Docker Setup



```bash

docker --version

```



Ensure Docker Desktop is running.



\---



\### 3) Kubernetes Setup (Docker Desktop)



\* Enable Kubernetes in Docker Desktop

\* Verify:



```bash

kubectl get nodes

```



\---



\### 4) Docker Hub Credentials in Jenkins



\* \*\*Kind\*\*: Username with password

\* \*\*ID\*\*: `dockerhub-creds`

\* Use a \*\*Docker Hub Access Token\*\* as password (recommended)



\---



\### 5) Jenkins Pipeline (from SCM)



In job configuration:



\* Definition: \*\*Pipeline script from SCM\*\*

\* SCM: \*\*Git\*\*

\* Repo: `https://github.com/srikanthpalem/demo-app.git`

\* Branch: `\*/main`

\* Script Path: `Jenkinsfile`



\---



\### 6) GitHub Webhook (via ngrok)



```bash

ngrok http 8080

```



\* Copy HTTPS URL (e.g., `https://xxxx.ngrok-free.dev`)

\* GitHub → Repo → Settings → Webhooks → Add:



&#x20; \* Payload URL: `https://<ngrok-url>/github-webhook/`

&#x20; \* Content type: `application/json`



Update \*\*Manage Jenkins → System → Jenkins URL\*\* to the ngrok URL.



\---



\### 7) Fix Kubernetes Access for Jenkins



Jenkins runs as a Windows service → needs kubeconfig.



\* Copy:



```text

C:\\Users\\<username>\\.kube\\config

→

C:\\ProgramData\\Jenkins\\.kube\\config

```



\* Set env in Jenkins (Manage Jenkins → System → Global properties):



```text

KUBECONFIG = C:\\ProgramData\\Jenkins\\.kube\\config

```



\* Restart Jenkins (Admin CMD):



```bash

net stop jenkins

net start jenkins

```



\---



\## 📜 Jenkinsfile (Core Stages)



\* Checkout

\* Build (Maven)

\* Build Docker Image

\* Push to Docker Hub

\* Deploy to Kubernetes



\---



\## 🚀 How It Works



1\. Developer pushes code to GitHub

2\. GitHub webhook triggers Jenkins

3\. Jenkins builds JAR using Maven

4\. Docker image is built \& pushed to Docker Hub

5\. Kubernetes deployment is applied

6\. Pods are restarted with latest image



\---



\## 🧪 Verification



\* Jenkins build triggers automatically on push

\* Docker image visible in Docker Hub

\* Kubernetes resources:



```bash

kubectl get pods

kubectl get svc

```



\---



\## 🐛 Issues Faced \& Fixes



\* ❌ Docker push denied → ✔ Added Docker Hub credentials

\* ❌ YAML not found → ✔ Pushed files to GitHub

\* ❌ Webhook not triggering → ✔ Used ngrok + SCM pipeline

\* ❌ Branch mismatch → ✔ Switched to `main`

\* ❌ Jenkinsfile missing → ✔ Added to repo root

\* ❌ K8s auth error → ✔ Configured kubeconfig for Jenkins

\* ❌ Groovy syntax error → ✔ Fixed quotes in Jenkinsfile



\---



\## 📈 Achievements



\* Fully automated CI/CD pipeline

\* Zero manual deployment

\* Real-world DevOps workflow implemented



\---



\## 🌍 Future Enhancements



\* Deploy on \*\*AWS EC2 + EKS\*\*

\* Use \*\*Helm Charts\*\*

\* Add \*\*CI testing stage\*\*

\* Add \*\*Monitoring (Prometheus + Grafana)\*\*

\* Use \*\*private container registry\*\*



\---



\## 👨‍💻 Author



\*\*Srikanth Palem\*\*



\---



\## ⭐ Resume Impact



\* Built an end-to-end CI/CD pipeline using Jenkins, Docker, and Kubernetes

\* Implemented GitHub webhook-based automation using ngrok

\* Deployed containerized applications to Kubernetes cluster

\* Solved real-world DevOps issues (authentication, SCM, pipeline errors)



\---



🚀 Ready for cloud deployment (AWS/EKS)



