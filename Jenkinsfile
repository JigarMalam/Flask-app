pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }
        stage('Test') {
            steps {
                sh 'pytest > result.log'
            }
        }
        stage('Deploy') {
            when {
                expression { currentBuild.result == null || currentBuild.result == 'SUCCESS' }
            }
            steps {
                echo 'Deploying to staging environment...'
                // Use SCP or Docker or any method you prefer
            }
        }
    }
    post {
        success {
            mail to: 'jigarmalam13@gmail.com',
                 subject: 'Build Success',
                 body: "Build #${env.BUILD_NUMBER} succeeded."
        }
        failure {
            mail to: 'jigarmalam13@gmail.com',
                 subject: 'Build Failed',
                 body: "Build #${env.BUILD_NUMBER} failed. Please check Jenkins."
        }
    }
}
