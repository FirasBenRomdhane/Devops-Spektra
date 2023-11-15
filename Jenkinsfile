pipeline {
    agent any
    stages {
        stage('Launching SonarQube') {
            steps {
                sh 'docker compose up -d sonarqube'
            }
        }
        stage('Building') {
            steps {
                sh 'mvn clean'
                sh 'mvn compile'
                sh 'mvn package'
            }
        }
        stage('Code Quality check') {
            steps {
                sh "mvn sonar:sonar -Dsonar.login=${params.SONAR_LOGIN} -Dsonar.password=${SONAR_PWD} -Dsonar.host.url=http://localhost:9000"
            }
        }

        stage('Building and pushing docker image') {
            steps {
                sh "docker build -t ${params.DOCKERHUB_USERNAME}/${params.IMG_NAME}:${IMG_TAG} /usr/app"
                sh "docker login -u ${params.DOCKERHUB_USERNAME} -p ${params.DOCKERHUB_PWD}"
                sh "docker push ${params.DOCKERHUB_USERNAME}/${params.IMG_NAME}:${IMG_TAG}"
            }
        }
        stage('NEXUS DEPLOY') {
            steps {
                sh 'mvn deploy'
            }
        }
        stage('Running Application') {
            steps {
                sh 'docker compose up -d app-achat mysqldb'
            }
        }
        stage('Running Monitoring services') {
            steps {
                sh 'docker compose up -d prometheus grafana'
            }
        }
    }
}
