node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email vishal.n.patel1909@gmail.com"
                        sh "git config user.name Vishal Patel"
                        //sh "git switch master"
                        sh "cat ./dev/deployment.yaml"
                        sh "sed -i 's+vishal4590/demo-helloworld.*+vishal4590/demo-helloworld:${DOCKERTAG}+g' ./dev/deployment.yaml"
                        sh "cat ./dev/deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/demo-helloworld-k8s.git HEAD:main"
      }
    }
  }
}
}