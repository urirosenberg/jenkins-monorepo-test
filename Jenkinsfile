pipeline {
    agent any

    stages {
        stage('Detect changes') {
            steps {
                echo 'Detect changes'
                script {
                    changed_components = sh (
                        script: "git diff --name-only $GIT_PREVIOUS_COMMIT $GIT_COMMIT | awk 'BEGIN {FS=\"/\"} {print \$1}' | uniq",
                        returnStdout: true).trim()
                }
                echo "Changed_components: ${changed_components}"

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
