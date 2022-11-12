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
                        sh "git config user.email yadavrohit2709@gmail.com"
                        sh "git config user.name yadavrohit2709"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+126900832762.dkr.ecr.us-east-1.amazonaws.com/ecs-ecom-repository.*+126900832762.dkr.ecr.us-east-1.amazonaws.com/ecs-ecom-repository:${IMAGETAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${IMAGETAG}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesmanifest.git HEAD:main"
      }
    }
  }
}
}
