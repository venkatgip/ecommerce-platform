pipeline {
    agent any

    tools {
        jdk 'JAVA_HOME'   // Use the JDK you configured in Jenkins (e.g., JDK 17+)
    }

    options {
        timestamps()
       //ansiColor('xterm')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/venkatgip/ecommerce-platform.git'
            }
        }

        stage('Build') {
            steps {
                // Use Gradle wrapper to ensure version consistency (Gradle 8.8)
                bat 'gradle clean build --no-daemon --warning-mode all'
            }
        }

        stage('Test') {
            steps {
                bat 'gradle test --no-daemon'
            }
        }

        stage('Run User Service') {
            steps {
                bat 'gradle :user-service:run --no-daemon'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: '**/build/libs/*.jar', fingerprint: true
            }
        }
    }

    post {
        always {
            junit '**/build/test-results/test/*.xml'
        }
        success {
            echo '✅ Build and Tests successful!'
        }
        failure {
            echo '❌ Build failed. Check logs.'
        }
    }
}
