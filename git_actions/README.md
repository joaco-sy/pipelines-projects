This is a GitLab CI/CD pipeline configuration file. It automates the deployment of a Java web application to multiple servers (svr01.devprov, svr02.devprov, and svr03.devprov) running Tomcat. Let's break down the configuration step by step:

    Stages:

    yaml

stages:
  - deploy

This pipeline has only one stage, named "deploy." The jobs defined within this stage will be executed sequentially.

Workflow Rules:

yaml

workflow:
  rules:
    - if: '$CI_PIPELINE_SOURCE == "web"'
      when: always
    - when: never

These workflow rules determine when the pipeline should be executed. If the pipeline is triggered from a web source ($CI_PIPELINE_SOURCE == "web"), it will always run. Otherwise, if triggered from any other source, it will never run.

Variables:

yaml

variables:
  SECURE_FILES_DOWNLOAD_PATH: '.'
  VAR:
    value: "hello"
    description: "pruebadesc"

These are environment variables used in the pipeline. SECURE_FILES_DOWNLOAD_PATH is set to the current directory, and VAR is defined with the value "hello" and a description "pruebadesc."

.deploy_template:

yaml

.deploy_template:
  before_script:
    - shopt -s expand_aliases
    - alias ssh='ssh -i id_rsa -o StrictHostKeyChecking=no'
    - alias scp='scp -i id_rsa -o StrictHostKeyChecking=no'
    - download-secure-files
    - chmod 0600 id_rsa

This is a job template, defined using YAML anchors (starts with .). It contains a set of commands that will be executed before any of the jobs that extend this template. The commands set up some aliases for ssh and scp, download secure files, and change permissions on the id_rsa file.

Deploy Jobs (deploy_svr01, deploy_svr02, deploy_svr03):
Each deploy job follows the same structure, but they target different servers.

a. deploy_svr01:

yaml

    deploy_svr01:
      stage: deploy
      extends: .deploy_template
      script:
        - ssh root@svr01.devprov "systemctl stop tomcat"
        - ssh root@svr01.devprov "cp /usr/share/tomcat/webapps/new_war.war ~/bkp"
        - ssh root@svr01.devprov "rm -rf /usr/share/tomcat/webapps/*"
        - scp new_war.war root@svr01.devprov:/usr/share/tomcat/webapps/new_war.war
        - ssh root@svr01.devprov "chown -R tomcat:tomcat /usr/share/tomcat/webapps"
        - ssh root@svr01.devprov "systemctl start tomcat"

    This job is responsible for deploying the web application to svr01.devprov. It extends the .deploy_template defined earlier, which means the commands in the before_script section of the template will be executed before the job's script.

    The script for this job stops Tomcat, backs up the current application (if any), removes existing web applications, copies the new new_war.war to the Tomcat webapps directory, changes ownership, and starts Tomcat.

    b. deploy_svr02, deploy_svr03:
    The deploy_svr02 and deploy_svr03 jobs follow the same structure as deploy_svr01, but they target different servers (svr02.devprov and svr03.devprov, respectively).

In summary, this pipeline automates the deployment of a Java web application to three different servers running Tomcat. It leverages job templates to avoid duplication of commands and executes specific deployment steps for each server in separate jobs. The pipeline ensures that Tomcat is stopped, the new WAR file is deployed, and Tomcat is started again on each server during the deployment process.