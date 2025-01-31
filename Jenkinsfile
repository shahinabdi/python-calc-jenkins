pipeline {
    agent any
    
    stages {
        stage('Setup Python') {
            steps {
                script {
                    sh 'python3 -m pip install --upgrade pip'
                    sh 'pip install -r requirements.txt'
                }
            }
        }
        
        stage('Run Tests') {
            steps {
                script {
                    sh 'python3 -m pytest test_calculator.py -v'
                }
            }
        }
        
        stage('Build Development') {
            when {
                branch 'develop'
            }
            steps {
                echo 'Building development version...'
                script {
                    sh 'python3 -m py_compile calculator.py'
                    // Add development-specific steps here
                    sh 'echo "Version: Dev-${BUILD_NUMBER}" > version.txt'
                }
            }
        }
        
        stage('Build Production') {
            when {
                branch 'main'
            }
            steps {
                echo 'Building production version...'
                script {
                    sh 'python3 -m py_compile calculator.py'
                    // Add production-specific steps here
                    sh 'echo "Version: Prod-${BUILD_NUMBER}" > version.txt'
                }
            }
        }
        
        stage('Deploy to Development') {
            when {
                branch 'develop'
            }
            steps {
                echo 'Deploying to development environment...'
                // Add your development deployment steps here
            }
        }
        
        stage('Deploy to Production') {
            when {
                branch 'main'
            }
            steps {
                echo 'Deploying to production environment...'
                // Add your production deployment steps here
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}