pipeline {
        agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
        }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package -Denforcer.skip=true'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test -Denforcer.skip=true'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
