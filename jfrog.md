

##  **Architecture**

    Developer → EC2 (Ubuntu) → Artifactory Service → Browser Access via Port 8081

***

##  **Prerequisites**

*   AWS EC2 Instance (Ubuntu 20.04 / 22.04)
*   Ports Open: **8081** (Artifactory UI)
*   Internet Access
*   `sudo` privileges on EC2

***

##  **1. Update System**

```bash
sudo apt update -y
sudo apt upgrade -y
```

***

##  **2. Install Java (Required for Artifactory)**

```bash
sudo apt install openjdk-11-jdk -y
```

Verify Java:

```bash
java -version
```

***

##  **3. Add JFrog GPG Key & Repository**

```bash
wget -qO - https://releases.jfrog.io/artifactory/api/gpg/key/public | sudo apt-key add -
```

Add repo:

```bash
echo "deb https://releases.jfrog.io/artifactory/jfrog-artifactory-debs focal main" \
| sudo tee /etc/apt/sources.list.d/jfrog.list
```

Update:

```bash
sudo apt update -y
```

***

##  **4. Install Artifactory OSS**

```bash
sudo apt install jfrog-artifactory-oss -y
```

Or Pro version:

```bash
sudo apt install jfrog-artifactory-pro -y
```

***

##  **5. Start & Enable Artifactory Service**

```bash
sudo systemctl start artifactory
sudo systemctl enable artifactory
sudo systemctl status artifactory
```

***

##  **6. Configure Security Group (AWS)**

Open inbound rule:

| Type       | Protocol | Port | Source    |
| ---------- | -------- | ---- | --------- |
| Custom TCP | TCP      | 8081 | 0.0.0.0/0 |

***

##  **7. Access Artifactory UI**

Open browser and go to:

    http://<EC2-PUBLIC-IP>:8081/artifactory

Follow GUI onboarding steps.

***

##  (Optional) **8. Configure NGINX Reverse Proxy**

Install:

```bash
sudo apt install nginx -y
```

Configure proxy:

```bash
sudo /opt/jfrog/artifactory/app/bin/artifactory-configure-nginx
```

Restart:

```bash
sudo systemctl restart nginx
```

***

##  (Optional) **9. File Paths**

| Component    | Path                               |
| ------------ | ---------------------------------- |
| Config files | `/opt/jfrog/artifactory/var/etc/`  |
| Logs         | `/opt/jfrog/artifactory/var/log/`  |
| Data         | `/opt/jfrog/artifactory/var/data/` |

***

##  **10. Verify Installation**

```bash
curl http://localhost:8081/artifactory/api/system/ping
```

Expected response:

    OK

***

## 📤 **Uninstall Artifactory**

```bash
sudo apt remove jfrog-artifactory-oss -y
sudo rm -rf /opt/jfrog
```

***

## ✔️ **Conclusion**

Your JFrog Artifactory instance is now successfully installed on your EC2 server and accessible through the browser.

***


