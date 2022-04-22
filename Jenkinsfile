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
