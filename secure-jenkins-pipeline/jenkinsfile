pipeline {
    tools {
        maven 'Maven'
    }
    agents any
    stages {
        stage ('Inicio') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
        }

        stage ('Build') {
            sh 'mvn clean package'
        }
    }
}