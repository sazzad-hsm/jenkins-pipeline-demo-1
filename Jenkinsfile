pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps { //Checking out the repo
                checkout changelog: true, scm: [$class: 'GitSCM', branches: [[name: '*/master']], browser: [$class: 'github', repoUrl: 'https://github.com/lynaspublic/spring-demo']]
            }
        }
        stage('Unit & Integration Tests') {
            steps {
                script {
                    sh './gradlew clean test --no-daemon' //run a gradle task
                }
            }
        }
        stage('Frontend Unit Tests') {
            steps {
                sshagent(['git']) {
                    script {
                        sh './gradlew build --no-daemon'
                    }
                }
            }
        }
    }
}
