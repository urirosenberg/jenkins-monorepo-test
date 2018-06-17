pipeline {
    agent any

    stages {
        stage('Detect changes') {
            steps {
               // Git committer email
                GIT_COMMIT_EMAIL = sh (script: 'uname',returnStdout: true)
                echo "Git committer email: ${GIT_COMMIT_EMAIL}"
            }
        }
        stage('Build') {
            steps {
                echo 'Building..'
                echo "${GIT_COMMIT_EMAIL}"
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
