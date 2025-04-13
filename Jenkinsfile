pipeline {
    agent { label 'Jenkins-Agent' }
    tools {
        jdk 'Java17'
        maven 'Maven3'
    }
    
    stages{
        stage("Cleanup Workspace"){
                steps {
                cleanWs()
                }
        }

        stage("Checkout from SCM"){
                steps {
                    git branch: 'main', credentialsId: 'github', url: 'https://github.com/Jeremias1420/register-app.git'
                }
        }

        stage("Build Application"){
            steps {
                sh "mvn clean package"
            }

       }

       stage("Test Application"){
           steps {
                 sh "mvn test"
           }
       }
     stage("SonarQube Analysus"){
         steps{
             script {
                 withSonarQubeEnv (credentailsId: 'jenkins-sonarqube-token' ) {
                 sh "mvn sonar: sonar"
                 }
             }
        }
     }
   }
}
