pipeline {
    agent any
    stages {
        // Build Stage
        stage('Build') {
            steps {
                withMaven(maven: 'mvn-3.6.3') {
                    sh 'mvn -B -DskipTests clean package'
                }
            }
        }
        stage('Test') {
            steps {
                withMaven(maven: 'mvn-3.6.3') {
                    sh 'mvn test'
                }
            }
        }
        stage ('Results'){
            parallel {
                stage ('Junit') {
                    steps {
                        junit 'target/surefire-reports/*.xml'
                    }
                }
                stage('Deliver') {
                    steps {
                        sh './jenkins/scripts/deliver.sh'
                    }
                }
            }
        }
    }
}
