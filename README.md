![Starbucks Clone Deployment](https://github.com/user-attachments/assets/6b654f47-9537-4b88-9584-41c760fc49ac)

# Deploy Starbucks Clone Application in Digital OCean using DevSecOps Approach

# ** Resources Used **
- 2 * Droplets ( 4vcpu/ 8GB memory/ Ubuntu 24.04 LTS)
- Digital Ocean Kubernetes Cluster (Cluster capacity - 3 * droplets (4GB memory/2vcpus)

# ** Tools & Services Used **

- **GitHub** ![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)
- **Jenkins** ![Jenkins](https://img.shields.io/badge/Jenkins-D24939?style=flat-square&logo=jenkins&logoColor=white)
- **SonarQube** ![SonarQube](https://img.shields.io/badge/SonarQube-4E9BCD?style=flat-square&logo=sonarqube&logoColor=white)
- **Docker** ![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
- **OWASP** ![OWASP](https://img.shields.io/badge/OWASP-000000?style=flat-square&logo=owasp&logoColor=white)
- **Trivy** ![Trivy](https://img.shields.io/badge/Trivy-00979D?style=flat-square&logo=trivy&logoColor=white)

# **Install doctl**
```
reference document - https://docs.digitalocean.com/reference/doctl/how-to/install/
```
 
# **Install Jenkins on Ubuntu:**

```
reference document - https://www.jenkins.io/doc/book/installing/linux/
```


# **Install Docker on Ubuntu:**
```
reference document - https://docs.docker.com/engine/install/ubuntu/

add permission to user to use docker (without root privilegdes) -- sudo usermod -aG docker $USER

login to dockerhub account using -- docker login -u <username>

install docker compose -
sudo curl -L "https://github.com/docker/compose/releases/download/v2.20.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

install docker scout and allow permission to docker socket to be used by jenkins
sudo chmod 777 /var/run/docker.sock
curl -sSfL https://raw.githubusercontent.com/docker/scout-cli/main/install.sh | sh -s -- -b /usr/local/bin 

```

# **Install Trivy on Ubuntu:**
```
Reference Doc: https://aquasecurity.github.io/trivy/v0.55/getting-started/installation/
```



# Deployment Stages: (Credit to @amonkincloud for the pipeline diagram and code)
<img width="966" alt="Screenshot 2024-09-15 at 7 20 49 AM" src="https://github.com/user-attachments/assets/ddb5e618-79ab-49b3-8f13-b5114824eec3">


# Jenkins Complete pipeline
```
Provided in Jenkinsfile

```
