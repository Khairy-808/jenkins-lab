pipeline {
    agent { label 'php-agent' }

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning source code from GitHub...'
                checkout scm
            }
        }

        stage('Verify Tools') {
            steps {
                sh '''
                    echo "Checking PHP version..."
                    php -v

                    echo "Checking PHPUnit version..."
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
            echo '✅ Build succeeded. All unit tests passed.'
        }

        failure {
            echo '❌ Build failed. One or more tests failed.'
        }

        always {
            echo 'Pipeline finished.'
        }
    }
}
