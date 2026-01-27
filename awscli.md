
***

# ** Installing AWS CLI v2 on Ubuntu (EC2 + Local Machine)**

AWS CLI v2 is the recommended version for all modern AWS operations, including S3, EC2, IAM, CloudWatch, Lambda, and automation scripts.  
This README provides a **clean, step‑by‑step installation guide** that works on **all Ubuntu versions**, including minimal EC2 AMIs where `awscli` APT package is NOT available.

***

***

#  **Step 1 — Remove Any Previous/Incompleted Installations**

```bash
sudo rm -rf aws
sudo rm -rf /usr/local/aws-cli
sudo rm -f awscliv2.zip
```

This ensures you start clean.

***

#  **Step 2 — Download AWS CLI v2 Installer**

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
```

***

#  **Step 3 — Install unzip (if missing)**

```bash
sudo apt update
sudo apt install unzip -y
```

***

#  **Step 4 — Unzip the Installer Package**

```bash
unzip awscliv2.zip
```

This creates a directory named `aws/`.

***

#  **Step 5 — Install AWS CLI v2**

```bash
sudo ./aws/install
```

If updating an old installation:

```bash
sudo ./aws/install --update
```

This installs the CLI into:

*   `/usr/local/bin/aws`
*   `/usr/local/aws-cli/`

***

#  **Step 6 — Verify Installation**

```bash
aws --version
```

Expected output example:

    aws-cli/2.17.23 Python/3.11.0 Linux/x86_64

If you still see **command not found**, update your PATH:

```bash
echo 'export PATH=/usr/local/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```

Then verify again:

```bash
aws --version
```

***

#  **(Optional) Step 7 — Configure AWS CLI**

If you want to use Access Keys:

```bash
aws configure
```

Enter:

*   AWS Access Key ID
*   AWS Secret Access Key
*   Region (example: `ap-south-1`)
*   Output format (`json`)

***

#  Recommended: Use IAM Role on EC2 (No Keys Required)

If your EC2 instance has an IAM role attached, AWS CLI works automatically:

Test:

```bash
aws sts get-caller-identity
```

***

# 🧪 **Example: Copy File From S3 to EC2**

Once AWS CLI is installed, run:

```bash
aws s3 cp s3://pem-webserver/prod.pem /home/ubuntu/prod.pem
chmod 400 /home/ubuntu/prod.pem
```

***

# 🧹 **Uninstall AWS CLI v2**

```bash
sudo /usr/local/aws-cli/bin/aws --version
sudo /usr/local/aws-cli/bin/aws uninstall
```

***

# 🎉 **AWS CLI v2 Installed Successfully!**

You can now run all AWS operations:

```bash
aws s3 ls
aws ec2 describe-instances
aws iam list-users
```

***


