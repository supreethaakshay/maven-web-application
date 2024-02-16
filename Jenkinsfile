node{
    
    echo "Build number: ${env.BUILD_NUMBER}"
    echo "Job name: ${env.JOB_NAME}"
    echo "Node name: ${env.NODE_NAME}"

    def mavenHome= tool name: "maven3.9.6"

    properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])

    stage('CheckoutCode'){
        git branch: 'development', credentialsId: 'a15207fe-e84d-4f24-b33d-8bb0832777f7', url: 'https://github.com/supreethaakshay/maven-web-application.git'
    }

    stage('Build'){
        sh "${mavenHome}/bin/mvn clean package"
    }
    /*
    stage('ExecuteSonarQubeReport'){
        sh "${mavenHome}/bin/mvn sonar:sonar"
    }

    stage('UploadArtifactintoNexus'){
        sh "${mavenHome}/bin/mvn deploy"
    }

    stage('DeployApplicationintoTomcatServer'){
        sshagent(['4b36fe16-514b-4269-b09d-79e068e715c6']) {
            sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@172.31.3.186:/opt/apache-tomcat-9.0.83/webapps"
}
    }
    
*/
  
}//Node Closing
