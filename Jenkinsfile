pipeline {
    agent any
        tools {
        gradle 'GRADLE_HOME'   // Use your configured Gradle tool name
        jdk 'JAVA_HOME'        // Use your configured JDK tool name
    }
    stages {
        stage('Checkout') {
            steps {
                // Replace with your repo URL if needed
                git url: 'https://github.com/venkatgip/ecommerce-platform.git', branch: 'master'
            }
        }
        stage('Build') {
            steps {
                // For Maven projects
                //sh 'mvn clean package -DskipTests'
                // For Gradle:
                 bat 'gradle clean build -x test'
            }
        }
        stage('Test') {
            steps {
                // For Maven
               //sh 'mvn test'
                // For Gradle:
                 bat 'gradle test'
            }
           
        }
        stage('Deploy') {
            steps {
                // Add commands for deployment, e.g., file copy, docker build, etc.
                echo 'Deploy stage - add deployment scripts here'
            }
        }
    }

    post {
        success {
            echo 'Build and Deploy succeeded!'
        }
        failure {
            echo 'Build or Deploy failed!'
        }
    }
}
