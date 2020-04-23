pipeline {
    agent any
    stages {
        stage('Build Stage') {
            steps {
                echo "We are at Building..."
                bat "ruby hello.rb"
                bat "powershell.exe Compress-Archive  hello.rb Hello-1.0.%BUILD_NUMBER%.zip"
                echo "Building finished!"
            }
        }
        stage('Testing Stage') {
            steps {
                echo "Testing..."
                echo "Testing finished!"
            }
        }
        stage('Deployment Stage') {
            steps {
                echo "Deploying..."
                echo "Deploying finished"
            }
        }
        
    }
    post {
        always {
            bat "jfrog rt c artifactory-demo --url=http://172.18.0.100:8081/artifactory --user=admin --password=ti1w2ratp.TimAp"
            bat "jfrog rt u Hello-1.0.%BUILD_NUMBER%.zip generic-local"
            echo 'We came to an end!'
        }
        success {
            echo 'Build is Successful brother!'
        }
        failure {
            echo 'Sorry mate! Build is Failed! :('
        }
        unstable {
            echo 'Run was marked as unstable'
        }
        changed {
            echo 'Hey look at this, Pipeline state is changed.'
        }
    }
}
