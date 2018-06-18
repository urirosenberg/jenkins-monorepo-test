pipeline {
    agent any

    stages {
        stage('Detect changes') {
            steps {
                echo 'Detect changes'

                script {
                    IGNORE_FILES = sh (
                        script: "ls -p | grep -v /",
                        returnStdout: true).trim()
                }
                script {
                    IGNORE_FILES=IGNORE_FILES.split("/n")
                }

                //detect changed directories
                script {
                    changed_components = sh (
                        script: "git diff --name-only $GIT_PREVIOUS_COMMIT $GIT_COMMIT | awk 'BEGIN {FS=\"/\"} {print \$1}' | uniq",
                        returnStdout: true).trim()
                }
                script {
                    changed_components=changed_components.split("/n")
                }
                echo "Changed_components: ${changed_components}"
            }
        }

        stage ('Main Build Stage') {
            steps {
                script {
                    for(compName in changed_components){
                        if (!(compName in IGNORE_FILES)) {
                            stage ('Stage ${compName}') {
                                sh 'echo Stage ${compName}'
                            }
                        }
                        else{
                            sh 'echo Stage ${compName}'
                        }
                    }
                }
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
