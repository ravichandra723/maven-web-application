node{

def mavenHome = tool name: "maven3.8.5"

//Checkout Stage
stage('CheckoutCode'){
 git branch: 'development', credentialsId: '5393154b-7ae5-43c6-b74a-12c3a25e5a1a', url: 'https://github.com/ravichandra723/maven-web-application.git'
}

//Build Stage
stage('Build'){
sh "$mavenHome/bin/mvn clean package"
}

//Generate SonarQube Report
stage('SonarQubeReport'){
sh "$mavenHome/bin/mvn sonar:sonar"
}

//Upload Artifact into Artifactory repo
stage('UploadArtifactintonexus'){
sh "$mavenHome/bin/mvn deploy"
} 
//Deploy App into Tomcat Server
stage('DeployAppIntoTomcat'){
sshagent(['8f57d6ff-e877-44af-8b38-c2d899864c37']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.233.19.251:/opt/apache-tomcat-9.0.60/webapps"
}
}


}//Node Closing
