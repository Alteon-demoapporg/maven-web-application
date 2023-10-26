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
      sshagent(['5b773cc9-beff-4629-b31b-9741a18652b9']) {
          
          sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@54.162.82.56:/opt/tomcat/webapps/"
    
}
        
    }
    stage('Email'){
        emailext body: '''Build Done!!!

Regards,
Pravallika B''', subject: 'Build Done!!', to: 'bpravalikaraj52@gmail.com'
        
    }
}
