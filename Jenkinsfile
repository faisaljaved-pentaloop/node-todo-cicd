pipeline{
    agent {label 'dev-agen-new'}
    stages {
        stage ('code') {
            steps {
                git url: 'https://github.com/faisaljaved-pentaloop/node-todo-cicd.git' , branch: 'master'
            }
        }
        stage ('build and test') {
            steps {
                sh 'docker build . -t faisaldevopsengg/node-todo-app-cicd:latest'
            }
        }
         stage ('login and push image') {
            steps {
                echo 'login and push image'
                withCredentials([usernamePassword(credentialsId: 'dockerhub-id', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                    sh "docker push faisaldevopsengg/node-todo-app-cicd:latest"
                }
        
            }
        }
        stage ('deploy') {
            steps {
                sh 'docker-compose down && docker-compose up -d'
            }
        }
    }
}
