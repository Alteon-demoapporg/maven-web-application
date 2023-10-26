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
      sshagent(['28647c27-3f72-4d27-bc8a-2d1323894abc']) {
          
          sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@18.220.175.181:/opt/apache-tomcat-9.0.80/webapps/"
    
}
        
    }
    stage('Email'){
        emailext body: '''Build Done!!!

Regards,
Pravallika B''', subject: 'Build Done!!', to: 'bpravalikaraj52@gmail.com'
        
    }
}
