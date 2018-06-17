pipeline {
    agent any

    stages {
        stage('Detect changes') {
            steps {
                echo 'Detect changes'
                sh 'bash build/detect-changes.sh'
            }
        }
        stage('Build') {
            steps {
                echo 'Building..'
		sh 'cat README.md'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
