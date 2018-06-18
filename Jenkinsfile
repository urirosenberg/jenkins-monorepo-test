pipeline {
    agent any

    stages {
        stage('Detect changes') {
            steps {
                echo 'Detect changes'
                //detect changed directories
                script {
                    changed_components = sh (
                        script: "git diff --name-only $GIT_PREVIOUS_COMMIT $GIT_COMMIT | awk 'BEGIN {FS=\"/\"} {print \$1}' | uniq",
                        returnStdout: true).trim()
                }
                script {
                    println "*** Changed_components before: ${changed_components}"
                    changed_components=changed_components.split("\n")
                    println "*** Changed_components after: ${changed_components}"
                }
                echo "Changed_components: ${changed_components}"
            }
        }

        stage ('Main Build Stage') {
            steps {
                script {
                        if ('sub-a' in changed_components){
                            stage ('Stage build sub-a') {
                              steps{
                                    echo 'doing sub-a stuff'
                                }
                            }
                        }
                        else if ('sub-b' in changed_components){
                            stage ('Stage build sub-b') {
                                steps{
                                    echo 'doing sub-b stuff'
                                }
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
