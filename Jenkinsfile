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
                script {
                    changed_components=changed_components.split("/n")
                }
                echo "Changed_components: ${changed_components}"
            }
        }

        for (int i=0; i< 2; ++i) {  
            stage("Stage #"+i){
                steps{
                    print 'Hello, world $i!'
                }
            }
        }
    }
}