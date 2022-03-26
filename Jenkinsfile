node{
    def mavenHome = tool name: "maven3.8.5"
      stage('checkoutcode'){
    
    git branch: 'development', credentialsId: 'cf228a17-bb9e-4ca6-bef2-294fcca97253', url: 'https://github.com/Anil-devops-mithun-dec2021/maven-web-application.git'
}

         
        stage('Build'){
sh "${mavenHome}/bin/mvn clean package"
}
stage('ExecutesonarQubeReport'){
sh " ${mavenHome}/bin/mvn sonar:sonar"
}


stage('UploadArtifactIntoNexusRepo'){
sh " ${mavenHome}/bin/mvn deploy"
}

stage('DeployAppIntotomcat')
{
 sshagent(['5092734d-209e-4267-8a62-2112e88446d4']) {

   sh  "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.126.20.179:/opt/apache-tomcat-9.0.60/webapps/"

}
}
}
