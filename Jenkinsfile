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
