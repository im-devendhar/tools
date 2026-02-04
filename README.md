
***

# 📘 **DevOps Tools – Installation & Basic Commands**

*A complete reference guide for DevOps POCs.  
Includes installation commands, basic usage, and tool-by-tool sections.*

***

# 🗂️ Table of Contents

*   \#1-linux-basics
*   \#2-git
*   \#3-docker
*   \#4-kubernetes
*   \#5-jenkins
*   \#6-github-actions
*   \#7-ansible
*   \#8-terraform
*   \#9-maven
*   \#10-sonarqube
*   \#11-nginx
*   \#12-aws-cli
*   \#13-python--pip
*   \#14-nodejs--npm
*   \#15-helm
*   \#16-prometheus--grafana

***

# -----------------------------------------

# **1. Linux Basics**

### ✔ Common Commands

```bash
ls -l
cd /path
pwd
cp file1 file2
mv file1 newname
rm -rf folder
cat file.txt
grep "keyword" file.txt
tail -f /var/log/syslog
df -h
free -m
top
systemctl status nginx
```

***

# -----------------------------------------

# **2. Git**

### ✔ Install

```bash
sudo apt update
sudo apt install -y git
```

### ✔ Commands

```bash
git init
git clone <repo-url>
git status
git add .
git commit -m "message"
git push origin main
git pull
```

***

# -----------------------------------------

# **3. Docker**

### ✔ Install

```bash
sudo apt install -y docker.io
sudo systemctl enable docker
sudo usermod -aG docker $USER
```

### ✔ Commands

```bash
docker build -t myapp .
docker images
docker ps -a
docker run -d -p 8080:80 myapp
docker stop <id>
docker rm <id>
docker push username/myapp:tag
```

***

# -----------------------------------------

# **4. Kubernetes (kubectl)**

### ✔ Install

```bash
sudo snap install kubectl --classic
```

### ✔ Commands

```bash
kubectl get pods
kubectl get nodes
kubectl apply -f deployment.yaml
kubectl delete -f deployment.yaml
kubectl logs <pod>
kubectl describe pod <pod-name>
```

***

# -----------------------------------------

# **5. Jenkins**

### ✔ Install

```bash
sudo apt update
sudo apt install -y openjdk-17-jdk
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt update
sudo apt install -y jenkins
```

### ✔ Essential Jenkins Plugins

*   Git
*   GitHub
*   Pipeline
*   Blue Ocean
*   Docker & Docker Pipeline
*   SonarQube Scanner
*   Credentials Binding

***

# -----------------------------------------

# **6. GitHub Actions**

### ✔ Sample Workflow File

`.github/workflows/main.yml`

```yaml
name: CI Pipeline

on:
  push:
    branches: ["main"]

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
      - uses: actions/checkout@v3
      - name: Run Tests
        run: echo "Running tests..."
```

***

# -----------------------------------------

# **7. Ansible**

### ✔ Install

```bash
sudo apt update
sudo apt install -y ansible
```

### ✔ Commands

```bash
ansible all -m ping
ansible-playbook site.yml
```

***

# -----------------------------------------

# **8. Terraform**

### ✔ Install

```bash
sudo apt update && sudo apt install -y gnupg software-properties-common curl
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
sudo apt update
sudo apt install -y terraform
```

### ✔ Commands

```bash
terraform init
terraform plan
terraform apply -auto-approve
terraform destroy -auto-approve
```

***

# -----------------------------------------

# **9. Maven**

### ✔ Install

```bash
sudo apt install -y maven
```

### ✔ Commands

test

````

---

# -----------------------------------------
# **10. SonarQube**

### ✔ Run using Docker
```bash
docker run -d --name sonarqube -p 9000:9000 sonarqube:lts
````

***

# -----------------------------------------

# **11. Nginx**

### ✔ Install

```bash
sudo apt install -y nginx
```

### ✔ Commands

```bash
systemctl status nginx
systemctl restart nginx
```

***

# -----------------------------------------

# **12. AWS CLI**

### ✔ Install

```bash
sudo apt install -y awscli
```

### ✔ Configure

```bash
aws configure
```

***

# -----------------------------------------

# **13. Python & Pip**

### ✔ Install

```bash
sudo apt install -y python3 python3-pip
```

### ✔ Commands

```bash
python3 --version
pip3 install boto3
```

***

# -----------------------------------------

# **14. Node.js & npm**

### ✔ Install

```bash
sudo apt install -y nodejs npm
```

### ✔ Commands

```bash
npm install
npm start
npm run build
```

***

# -----------------------------------------

# **15. Helm**

### ✔ Install

```bash
curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash
```

### ✔ Commands

```bash
helm repo add stable https://charts.helm.sh/stable
helm install myapp stable/nginx
helm list
```

***

# -----------------------------------------

# **16. Prometheus & Grafana**

### ✔ Prometheus

```bash
docker run -d -p 9090:9090 prom/prometheus
```

### ✔ Grafana

```bash
docker run -d -p 3000:3000 grafana/grafana
```

***

# 

