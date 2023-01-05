pipeline {
    agent any
    stages {       
        stage('Update git') {
            steps {
                script {
                    catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE'){
                        withCredentials([usernamePassword(credentialsId: 'tuananh_github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]){
                        // withCredentials([usernamePassword(credentialsId: 'tuananh_github')]){
                            sh "git config user.email vantuananh2811@gmail.com"
                            sh "git config user.name 'tuananh281'"
                            // sh "git config --unset http.proxy"
                            sh "cat deployment.yaml"
                            sh "sed -i 's+tuannanhh/test-gitops:latest+tuannanhh/test-gitops:${DOCKERTAG}+g' deployment.yaml"
                            sh "cat deployment.yaml"
                            sh "git add ."
                            sh "git commit -m 'Done get update manifest version: ${env.BUILD_NUMBER}'"
                            // sh "echo ${GIT_PASSWORD}"
                            sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/deploy-cluster.git HEAD:main"
                        }
                    }
                }
            }
        }
    }
}
