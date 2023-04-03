pipeline {
    agent any
    stages {
        stage('Clone repository') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/testpp']], // branch to checkout
                    userRemoteConfigs: [[url: 'https://github.com/xiang-a-zhang-rakuten/maven-demo.git']] // repository URL
                ])
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Dependency Check') {
            steps {
                sh 'mvn org.owasp:dependency-check-maven:check -Dformat=XML'
                archiveArtifacts 'target/dependency-check-report.xml'
            }
        }
    }
}
