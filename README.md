create server which having minimun t2.large and ram 30gb
Installation of Jenkins
```
#!/bin/bash

# Install OpenJDK 17 JRE Headless
sudo apt update
sudo apt install openjdk-17-jdk


# Download Jenkins GPG key
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

# Add Jenkins repository to package manager sources
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

# Update package manager repositories
sudo apt-get update

# Install Jenkins
sudo apt-get install jenkins -y
```
Installation of Docker
```
#!/bin/bash

# Update package manager repositories
sudo apt-get update

# Install necessary dependencies
sudo apt-get install -y ca-certificates curl

# Create directory for Docker GPG key
sudo install -m 0755 -d /etc/apt/keyrings

# Download Docker's GPG key
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc

# Ensure proper permissions for the key
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add Docker repository to Apt sources
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
$(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Update package manager repositories
sudo apt-get update

sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
ry to pull some default image ----> docker pull hello-world ----> You will be able to pull the image. If you are unable to pull the image. Execute the below command to provide necessary permissions ----> sudo chmod 666 /var/run/docker.sock ----> docker pull hello-world ----> You will be able to pull the image

# Add jenkins user to docker group
```
sudo usermod -aG docker jenkins
```
# Restart Jenkins to apply changes
```
sudo systemctl restart jenkins
```
# Verify Jenkins can access Docker
```
sudo -u jenkins docker ps
```
# Update & Install Python pip 
```
sudo apt-get update
sudo apt-get install -y python3-venv python3-pip
```
# Install docker-compose on your Jenkins server:
```
sudo apt-get update
sudo apt-get install -y docker-compose-plugin
```
give permisions to the docker sock
```
chmod 666 /var/run/docker.sock
```
Installation of Trivy
```
#!/bin/bash
sudo apt-get install wget apt-transport-https gnupg
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | gpg --dearmor | sudo tee /usr/share/keyrings/trivy.gpg > /dev/null
echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] https://aquasecurity.github.io/trivy-repo/deb generic main" | sudo tee -a /etc/apt/sources.list.d/trivy.list
sudo apt-get update
sudo apt-get install trivy
```

