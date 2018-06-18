pipeline {
    agent any

    stages {
        stage('Detect changes') {
            steps {
                echo 'Detect changes'
                // script {
                //     IGNORE_FILES = sh (
                //         script: "ls -p | grep -v /",
                //         returnStdout: true).trim()
                // }
                // script {
                //     IGNORE_FILES=IGNORE_FILES.split("/n")
                // }

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
                        if ('sub-a' in changed_components){
                            stage ('Stage build sub-a') {
                                sh 'echo Stage sub-a'
                            }
                        }
                        else if ('sub-b' in changed_components){
                            stage ('Stage build sub-b') {
                                sh 'echo Stage sub-b'
                            }
                        }
                        else{
                            stage ('Stage Build All') {
                                sh 'echo Stage build all'
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
