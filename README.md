# Jenkins Pipeline
Jenkins is a self-contained, open source automation server which can be used to automate all sorts of tasks related to building, testing, and delivering or deploying software. Jenkins can be installed through native system packages, Docker, or even run standalone by any machine with a Java Runtime Environment (JRE) installed.

## Pipeline View 
![image](https://user-images.githubusercontent.com/40850370/202151018-8aae2127-f3b0-4f7b-a17d-a3b5a2c5b7c1.png)

## Pipeline Setup Commands 
 Dashboard > + New Item > [ Enter Pipeline Name ] > Pipeline

### Trigger Pipeline using github actions

 [ .github/workflows/trigger.yml ]  

 github > settings > seceret > add [ All secrets ]

```yaml
name: trigger jenkins job
on: [push]
jobs:

  build:
    name: Build
    runs-on: ubuntu-latest
    steps:
    - name: trigger single Job
      uses: appleboy/jenkins-action@master
      with:
        url:  ${{ secrets.URL }}    # Jenkins Url
        user: ${{ secrets.USER }}   # User Name
        token: ${{ secrets.TOKEN }} # Api Token 
        job: ${{ secrets.JOBS }}    # Pipeline Name    
```
### Configuration of Jenkins Pipeline Project
```yaml
Discard old builds:
    Check : Yes

GitHub project: 
    Project url: https://github.com/ketangangal/Jenkins-Pipeline-Template

Pipeline:
    Definition : Pipeline script from scm
        repository url: https://github.com/ketangangal/Jenkins-Pipeline-Template

    Branches to build:
        Branch Specifier (blank for 'any'): */main

    Script Path : .jenkins/Jenkinsfile

```
### API Token Configuration

 Dashboard > People > USER NAME > Configure

```yaml

API_Token:
    Current_token:
        Add_new_token: Name (Api) and save somewhere

```

### Manage Plugins
 Dashboard > Manage jenkins > Plugin Manager > Available

```yaml
Amazon ECR plugin:
Amazon Web Services SDK : EC2
Docker plugin: Version1.2.10
docker-build-step:
Docker Pipeline:
Docker Commons Plugin: 
CloudBees Docker Build and Publish plugin: Version
```

### Manage Credentials Settings
 Dashboard > Manage jenkins > Credentials > System > Global credentials(unrestricted) > + Add credentials

```yaml
kind: Seceret Text
Scope: Global
Secret: *******
ID: name
Description: any
```

## Jenkins Setup from scratch
Detailed installation > scripts/jenkins.sh

Java Installation 
```bash
sudo apt update
sudo apt install openjdk-11-jre
java -version
```

Install Jenkins
```bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```

Start Jenkins
```bash
sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins
```

Install suggested plugins - to install the recommended set of plugins, which are based on most common use cases.

