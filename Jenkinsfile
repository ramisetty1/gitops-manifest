node {
    def app

    stage('Clone repository') {
      

        checkout([$class: 'GitSCM',
        branches: [[name: '*/master']],
        extensions: [], userRemoteConfigs: [[url: 'https://github.com/ramisetty1/gitops-manifest.git']]])
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email ramisettysiva1@gmail.com"
                        sh "git config user.name siva"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+ramisetty32/flask.*+ramisetty32/flask:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/gitops-manifest.git HEAD:master"
                        //sh "git push -u origin master"
      }
    }
  }
}
}
