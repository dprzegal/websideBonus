pipeline {
 agent any
  stages {
    stage("git") {
      steps {
        sh 'echo "Check out GitHub"'
        git branch: 'main', url: 'https://github.com/dprzegal/websiteBonus.git'
      }
    }
   stage("deploy to staging env") {
      steps {
        sh 'echo "Deploy to Nginx webserver"'
        sh 'rsync -avh /var/lib/jenkins/workspace/pipelineBonus/* /var/www/staging_web/'
        echo "Build number is ${currentBuild.number}"
      }
    }
   stage("test") {
      steps {
       script {
         if (currentBuild.currentResult == 'SUCCESS') {
             echo "Init currentResult: ${currentBuild.currentResult}"
             echo "The build number is ${env.BUILD_NUMBER}"
             echo "You can also use \${BUILD_NUMBER} -> ${BUILD_NUMBER}"
             sh 'echo "I can access $BUILD_NUMBER in shell command as well."'
             echo "${env.BUILD_URL} has result success"
         } else {
          echo "Don't deploy on Prod. There is a failur on Staging env"
         }
       }
       }
    } 
    stage("approval") {
      steps { 
        input("Do you want to deploy the website?")
      }
    }    
   stage("deploy") {
      steps {
        sh 'echo "Deploy to Nginx webserver"'
        sh 'rsync -avh /var/lib/jenkins/workspace/pipelineBonus/* /var/www/html/'
      }
    }
  }
}
