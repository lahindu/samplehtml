pipeline {
    agent any
    stages {
        stage('BUILD') {
            steps {
                println "build stage"
                sh 'docker build . -t 202256309025.dkr.ecr.ap-southeast-1.amazonaws.com/sample-ecr:v1'
                withCredentials([usernamePassword(credentialsId: 'aws-ecr', passwordVariable: 'password', usernameVariable: 'username')]) {
                    sh 'docker login --username $username --password $password 202256309025.dkr.ecr.ap-southeast-1.amazonaws.com'
                }
                sh 'docker push 202256309025.dkr.ecr.ap-southeast-1.amazonaws.com/sample-ecr:v1'
            }
        }
        stage('DEPLOY') {
            steps {
                sh 'kubectl apply -f manifests/'
            }
        }
        stage('ClearDir') {
            steps {
                cleanWs()
            }
        }
    }
}
