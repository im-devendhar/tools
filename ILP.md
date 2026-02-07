
---

````md
# DevOps ILP-1 – Starting Tools After VM Reboot

---

##  Manual Start Commands (After VM Power ON)

Run the following commands **inside the Ubuntu VM**.

---

###  Gitea
```bash
sudo systemctl start gitea
sudo systemctl status gitea
````

---

###  Jenkins

```bash
sudo systemctl start jenkins
sudo systemctl status jenkins
```

---

###  SonarQube (Docker Container)

```bash
docker start sonarqube
docker ps
```

---

###  JFrog Artifactory (Docker Container)

```bash
sudo systemctl status artifactory
sudo systemctl start artifactory
sudo systemctl restart artifactory
sudo systemctl enable artifactory
```

---

###  Apache Tomcat

```bash
cd ~/apache-tomcat-9.0.86/bin
./startup.sh
```

Verify:

```bash
ps -ef | grep tomcat
```

---

###  Verify All Running Services (Ports Check)

```bash
ss -tulnp | grep -E '3000|8080|8081|9000'
```

Expected ports:

* **3000** → Gitea
* **8080** → Jenkins / Tomcat (inside VM)
* **8081** → JFrog Artifactory
* **9000** → SonarQube

---

##  Permanent Auto-Start Configuration (Recommended)

Configure this **once** so all tools start automatically after every VM reboot.

---

###  Enable Jenkins Auto-Start

```bash
sudo systemctl enable jenkins
```

---

###  Enable Gitea Auto-Start

```bash
sudo systemctl enable gitea
```

---

###  Enable Docker Auto-Start

```bash
sudo systemctl enable docker
```

---

###  Configure Docker Containers Auto-Restart

#### SonarQube

```bash
docker update --restart unless-stopped sonarqube
```

#### JFrog Artifactory

```bash
docker update --restart unless-stopped artifactory
```

---

###  Enable Apache Tomcat Auto-Start

Create Tomcat systemd service:

```bash
sudo nano /etc/systemd/system/tomcat.service
```

Paste:

```ini
[Unit]
Description=Apache Tomcat
After=network.target

[Service]
Type=forking
User=$USER
Group=$USER
Environment=JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
Environment=CATALINA_HOME=/home/$USER/apache-tomcat-9.0.86
Environment=CATALINA_BASE=/home/$USER/apache-tomcat-9.0.86
ExecStart=/home/$USER/apache-tomcat-9.0.86/bin/startup.sh
ExecStop=/home/$USER/apache-tomcat-9.0.86/bin/shutdown.sh
Restart=always

[Install]
WantedBy=multi-user.target
```

Enable and start Tomcat:

```bash
sudo systemctl daemon-reload
sudo systemctl enable tomcat
sudo systemctl start tomcat
```

---

##  Result After VM Reboot

| Tool              | Auto-Starts |
| ----------------- | ----------- |
| Gitea             |  Yes       |
| Jenkins           |  Yes       |
| SonarQube         |  Yes       |
| JFrog Artifactory |  Yes       |
| Apache Tomcat     |  Yes       |

---


```
