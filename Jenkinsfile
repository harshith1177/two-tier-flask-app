pipeline {
    
    agent any;
    
 stages {
     stage("code-gitclone"){
         steps{
             git url: "https://github.com/harshith1177/two-tier-flask-app.git" , branch : "master"
         }
     }
          stage("build"){
         steps{
             sh "docker build -t two-tier-flask-app ."
         }
     }
 
          stage("test"){
         steps{
             echo "Test stage!!"
         }
     }
        stage("Push"){
         steps{
             withCredentials([usernamePassword(
                 credentialsId:"dockerHubCreds",
                 passwordVariable: "dockerHubPass",
                 usernameVariable: "dockerHubUser"
                 )]){
                 
             
             sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
             sh "docker tag two-tier-flask-app  ${env.dockerHubUser}/two-tier-flask-app "
             sh "docker push ${env.dockerHubUser}/two-tier-flask-app:latest"
             
             }
         }
     }
        stage("deploy"){
         steps{
             sh "docker compose up -d --build flask-app"
         }
     }
 }   
    
    
    
}
