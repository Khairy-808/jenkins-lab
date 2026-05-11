pipeline {
    agent { label 'php-agent' }

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning repository...'
                checkout scm
            }
        }

        stage('Verify Tools') {
            steps {
                sh '''
                    echo "Checking PHP..."
                    php -v

                    echo "Checking PHPUnit..."
                    phpunit --version
                '''
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh '''
                    echo "Running PHPUnit tests..."
                    phpunit tests
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Build succeeded. All tests passed.'
        }

        failure {
            echo '❌ Build failed. Check the unit tests.'
        }

        always {
            echo 'Pipeline finished.'
        }
    }
}
