pipeline {
    agent any
    stages {
        stage('BUILD') {
            steps {
                println "build stage"
            }
        }
        stage('DEPLOY') {
            steps {
                sh 'kubectl apply -f manifests/deployment.yml '
            }
        }
        stage('ClearDir') {
            steps {
                cleanWs()
            }
        }
    }
}
