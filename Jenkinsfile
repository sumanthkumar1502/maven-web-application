node {

def mavenHome = tool name: "maven3.6.3"

stage('CheckoutCode'){
git branch: 'development', credentialsId: '30179025-aa5e-4bff-b8a5-f87c38596f38', url: 'https://github.com/sumanthkumar1502/maven-web-application.git'
}

stage('Build'){
sh "${mavenHome}/bin/mvn clean package"

}

stage('ExecuteSonarQubeReport')
{
sh "${mavenHome}/bin/mvn sonar:sonar"
}

stage('UploadArtifactsIntoNexus')
{
sh "${mavenHome}/bin/mvn deploy"
}

stage('DeployApplicationIntoTomcatServer')
{
sshagent(['e9cbdfae-790d-41cf-ba5c-e1aaff5089a7']) {
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.234.238.112:/opt/apache-tomcat-9.0.46/webapps/"    
}
}

}
