pipeline {
    agent any

    stages {
        stage('Detect changes') {
            steps {
                echo 'Detect changes'
                sh '''
                    folders=`git diff --name-only $GIT_PREVIOUS_COMMIT $GIT_COMMIT | awk 'BEGIN {FS="/"} {print $1}' | uniq`
                '''
            }
        }
        stage('Build') {
            steps {
                echo 'Building..'
                echo "${changed_components}"
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
