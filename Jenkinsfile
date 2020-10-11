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
                sh 'docker logout'
            }
        }
        stage('DEPLOY') {
            steps {
                sh "sed -i 's/IMAGETAG/v1/g' manifests/deployment.yml"
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
