# Jenkins with sonarqube integration

Work In Progress

[[_TOC_]]

---
## prerequisites

prerequisites:
 - The sonarqube scanner plugin
 - your brach source plugin

<details>
<summary>my Docker-compose.yml</summary>

Work In Progress - why this? i dunno

>       version: '3'
>       services:
>           jenkins:
>             container_name: jenkins
>             image: jenkins/jenkins:latest
>             image: docker.io/mguazzardo/myjenkins:0.2
>             ports:
>               - "8080:8080"
>             networks:
>               - net
>           sonarqube:
>             container_name: sonarqube
>             image: sonarqube:latest
>             image: docker.io/mguazzardo/mysonarqube:0.1
>             ports:
>               - "9000:9000"
>             environment:
>               SONARQUBE_USERNAME: admin
>               SONARQUBE_PASSWORD: mipassword
>             networks:
>             - net
>       networks:
>         net:

</details>

Installing and Configuring your Jenkins plugins
SonarQube Scanner plugin

1. From the Jenkins Dashboard, navigate to Manage Jenkins > Manage Plugins and install the SonarQube Scanner plugin.
2. Back at the Jenkins Dashboard, navigate to Credentials > System from the left navigation.
3. Click the Global credentials (unrestricted) link in the System table.
4. Click Add credentials in the left navigation and add the following information:
    - Kind: Secret Text
    - Scope: Global
    - Secret: Generate a token at User > My Account > Security in SonarQube, and copy and paste it here.
5. Click OK.
6. From the Jenkins Dashboard, navigate to Manage Jenkins > Configure System.
7. From the SonarQube Servers section, click Add SonarQube. Add the following information:
    - Name: Give a unique name to your SonarQube instance.
    - Server URL: Your SonarQube instance URL.
    - Credentials: Select the credentials created during step 4.
8. Click Save

Branch Source plugin


1. From the Jenkins Dashboard, navigate to Manage Jenkins > Manage Plugins and install the GitHub Branch Source plugin.
2. From the Jenkins Dashboard, navigate to Manage Jenkins > Configure System.
3. From the GitHub or GitHub Enterprise Servers section, add your GitHub server.
4. Click Save.


---
## jenkins configuration

Work In Progress

### title

#### title

---
## Sonarquebe configuration

Work In Progress

### title

#### title

> comment

```verde```

**negr**

<details>
<summary>asd</summary>

- asd
- asd
- asd

</details>

https://docs.sonarqube.org/latest/analyzing-source-code/ci-integration/jenkins-integration/