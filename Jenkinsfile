pipeline {
    agent any

    environment {// change the below to your jdk path
        JAVA_HOME = "C:\\Program Files\\Eclipse Adoptium\\jdk-17.0.15.6-hotspot"
        PATH = "${JAVA_HOME}\\bin;${env.PATH}"
    }

    stages {

        stage('Verify Environment') {
            steps {
                bat 'echo JAVA_HOME=%JAVA_HOME%'
                bat 'java -version'
            }
        }

        stage('Checkout') { //change the below path to TRH repositoy url.
            steps {
                git branch: 'master', url: 'https://github.com/TohRH1003/Practical_9.git'
            }
        }

        stage('Build') {
            steps {
                bat 'gradlew.bat clean build --no-daemon'
            }
        }

        stage('Test') {
            steps {
                bat 'gradlew.bat test --no-daemon'
            }
        }


        stage('Deploy') {
            steps {
                bat 'java -jar build\\libs\\hello-world-java-V1.0.jar'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up workspace'
            deleteDir()
        }
        success {
            echo 'Build succeeded!!!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}