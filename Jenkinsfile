pipeline {
    agent any

    stages {
        stage('Set build params') {
            steps {
                script {
                    ANALYTICS_PATH='/Users/urir/workspace/haystack/haystack-analytics'
                }
                script {
                    def cause = currentBuild.rawBuild.getCause(hudson.model.Cause$UserIdCause)
                    println "CAUSE ${cause}"
                }
            }
        }
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
                    changed_components=changed_components.split("\n")
                }
                echo "Changed_components: ${changed_components}"
            }
        }

        stage ('Main Build Stage') {
            steps {
                script {
                        if ('elasticsearch' in changed_components){
                            stage ('Stage build elasticsearch') {
                                    echo 'doing sub-a stuff'
                            }
                        }
                        else if ('haystack-ingest' in changed_components){
                            stage ('Stage build haystack-ingest') {
                                echo 'doing sub-b stuff'
                            }
                        }
                        else if ('haystack-dashboard' in changed_components){
                            stage ('Stage build haystack-dashboard') {
                                echo 'doing sub-b stuff'
                            }
                        }
                        else{
                            stage ('No pipeline') {
                                sh 'echo Changes not in analytics'
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
