pipeline {
    agent {
        docker {
            image 'bytecodetech/maven-npm' 
            args '-v /root/.m2:/root/.m2'
             
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm i java-properties'
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
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