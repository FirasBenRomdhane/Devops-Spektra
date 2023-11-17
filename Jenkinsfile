pipeline {
    agent any
    stages {
        stage('Launching Sonarqube') {
            steps {
                echo 'hola :)'
            //sh 'docker compose up -d sonarqube'
            //sleep(60)
            }
        }
        stage('Launching Monitoring services') {
            steps {
                echo 'hola :)'
            //sh 'docker compose up -d prometheus grafana'
            }
        }
        stage('Building Project') {
            steps {
                sh 'mvn clean'
                sh 'mvn compile'
                sh 'mvn package'
            }
        }

        stage('Code Quality check') {
            steps {
                echo 'hola'
            //sh "mvn sonar:sonar -Dsonar.login=${params.SONAR_LOGIN} -Dsonar.password=${SONAR_PWD} -Dsonar.host.url=http://localhost:9000"
            //sh 'docker compose down sonarqube'
            }
        }
        stage('Building and pushing docker image') {
            steps {
                echo "s"
                //sh "docker build -t ${params.DOCKERHUB_USERNAME}/${params.IMG_NAME}:${IMG_TAG} ."
                //sh "docker login -u ${params.DOCKERHUB_USERNAME} -p ${params.DOCKERHUB_PWD}"
                //sh "docker push ${params.DOCKERHUB_USERNAME}/${params.IMG_NAME}:${IMG_TAG}"
            }
        }

        stage('NEXUS DEPLOY') {
            steps {
                echo 'hola :)'
            //sh 'mvn deploy'
            }
        }
        stage('Launching Project') {
            steps {
                sh 'docker-compose up -d mysqldb'
                sleep(10)
                //sh 'docker compose up -d app-achat'
            }
        }
    }
    post {
            failure {
                script {
                    sh 'docker compose down'
                }
            }
    }
}
