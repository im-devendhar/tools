
***

# **README — Jenkins Installation on Ubuntu (Using 2026 Updated GPG Key)**


***

## ** Prerequisites**

*   Ubuntu 20.04 / 22.04 / 24.04
*   Sudo privileges
*   Internet connectivity

***

# ** Step 1 — Update System**

```bash
sudo apt update
sudo apt upgrade -y
```

***

# ** Step 2 — Install Java 17 (Required for Jenkins LTS)**

According to Jenkins LTS Java support matrix, Java 17 is supported. [\[get.jenkins.io\]](https://get.jenkins.io/debian-stable/)

```bash
sudo apt install openjdk-17-jdk -y
```

Verify:

```bash
java -version
```

***

# ** Step 3 — Remove Old Jenkins Keys & Repo (Important)**

```bash
sudo rm -f /usr/share/keyrings/jenkins-keyring.asc
sudo rm -f /etc/apt/sources.list.d/jenkins.list
```

***

# ** Step 4 — Add the New 2026 Jenkins Repository Signing Key**

(Official new key introduced in 2026 Jenkins releases) [\[jenkins.io\]](https://www.jenkins.io/blog/2025/12/23/repository-signing-keys-changing/)

```bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2026.key | \
  sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
```

***

# ** Step 5 — Add Jenkins Apt Repository (LTS)**

```bash
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
https://pkg.jenkins.io/debian-stable binary/" | \
sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
```

***

# ** Step 6 — Update Apt Index**

```bash
sudo apt update
```

This time, the GPG error will disappear because you’re using the correct updated key.

***

# ** Step 7 — Install Jenkins**

```bash
sudo apt install jenkins -y
```

***

# ** Step 8 — Start & Enable Jenkins Service**

```bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
sudo systemctl status jenkins
```

Status output should show:

    active (running)

***

# ** Step 9 — Access Jenkins Web UI**

Open:

    http://YOUR_SERVER_IP:8080

Retrieve the initial Admin Password:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Paste it into the Jenkins setup page → Install Suggested Plugins → Create Admin User.

***

# ** Optional — Allow Jenkins to Use Docker**

If you want Jenkins to build Docker images:

```bash
sudo usermod -aG docker jenkins
sudo systemctl restart docker
sudo systemctl restart jenkins
```

***

# ** Service Management Commands**

Restart Jenkins:

```bash
sudo systemctl restart jenkins
```

Stop Jenkins:

```bash
sudo systemctl stop jenkins
```

***

# ** Uninstall Jenkins**

```bash
sudo systemctl stop jenkins
sudo apt remove jenkins -y
sudo apt autoremove -y
```

***

# ** Jenkins Successfully Installed!**

This README uses the **correct 2026 signing key**, based on the Jenkins project’s official announcement about updated repository keys.  
This avoids the `NO_PUBKEY` error and ensures secure installation. [\[jenkins.io\]](https://www.jenkins.io/blog/2025/12/23/repository-signing-keys-changing/)

***


