node {
    
    def mavenHome=tool name: "maven3.6.3"
    
    stage('CheckoutCode'){
      git branch: 'developement', credentialsId: '100124e2-b992-4bd0-a01b-d4d9645b7dd3', url: 'https://github.com/Alteon-demoapporg/maven-web-application.git'
    }
    stage('build'){
        sh "${mavenHome}/bin/mvn clean package"
    }
    stage('ExecuteSonarQubeReport'){
        sh "${mavenHome}/bin/mvn sonar:sonar"
        
    }
    stage('UploadArtifactIntoNexus'){
                sh "${mavenHome}/bin/mvn deploy"

    }
    stage('DeployAppIntoTomcatServer'){
      sshagent(['8334f68d-18b2-46b9-8f8e-8fff2819cd49']) {
          
          sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@http://18.234.129.50/:/opt/tomcat/webapps/"
    
}
        
    }
    stage('Email'){
        emailext body: '''Build Done!!!

Regards,
Pravallika B''', subject: 'Build Done!!', to: 'bpravalikaraj52@gmail.com'
        
    }
}
