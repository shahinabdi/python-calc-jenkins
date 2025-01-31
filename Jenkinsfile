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
    }
    
    post {
        success {
            echo 'Tests passed successfully!'
        }
        failure {
            echo 'Tests failed!'
        }
    }
}