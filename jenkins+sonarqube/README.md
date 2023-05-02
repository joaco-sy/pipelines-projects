# Jenkins with sonarqube integration

Work In Progress

[[_TOC_]]

---
## Docker configuration

<details>
<summary>Docker-compose.yml</summary>

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