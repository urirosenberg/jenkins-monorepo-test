pipeline {
    agent any

    stages {
        stage('Detect changes') {
            steps {
                echo 'Detect changes'
                changed_components = sh (
                    script: `git diff --name-only $GIT_PREVIOUS_COMMIT $GIT_COMMIT | awk 'BEGIN {FS="/"} {print $1}' | uniq`,
                    returnStatus: true
                ) == 0
                echo "changed_components flag: ${changed_components}"

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
