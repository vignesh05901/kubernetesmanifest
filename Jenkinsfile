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
                        bat "git config user.email vignesh0590@gmail.com"
                        bat "git config user.name vignesh05901"
                        //sh "git switch master"
                        bat "whoami"
                        bat "more deployment.yaml"
                        bat "powershell.exe -Command "(gc C:\tools\Jenkins\jenkins_home\workspace\ten_gitopsdemo_updatemanifest\deployment.yaml) -replace 'vignesh0590/gitops.*', 'vignesh0590/gitops:${DOCKERTAG}' | Out-File -encoding ASCII C:\tools\Jenkins\jenkins_home\workspace\ten_gitopsdemo_updatemanifest\deployment.yaml"
                        bat "more deployment.yaml"
                        bat "git add ."
                        bat "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        bat "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesmanifest.git HEAD:main"
      }
    }
  }
}
}
