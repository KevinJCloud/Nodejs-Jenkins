pipeline{
  agent any
  tools{
   nodejs "node"
  }

  stages{
   stage( "git checkout"){
     steps{
      script {
        checkout scmGit(branches: [[name: '*/main']],
        extensions: [],
        userRemoteConfigs: [[url: 'https://github.com/KevinJCloud/Nodejs-Jenkins.git']])
      }
     }
   }

   stage( "Node build"){
     steps{
      script {
        bat "npm install"
      }
     }
   }

   stage( "Docrizing the npm build"){
     steps{
      script {
        bat "docker build -t kevinjcloud/nodejs:v1 ."
      }
     }
   }

   stage( "Pushing docker image to docker registry"){
     steps{
      script {
             withCredentials([string(credentialsId: 'Docker-Passwd', variable: 'Password')]) {
             bat "docker login -u kevinjcloud -p %Password%"
              bat "docker push kevinjcloud/nodejs:v1"
         }
      }
     }
   }

  }
}
