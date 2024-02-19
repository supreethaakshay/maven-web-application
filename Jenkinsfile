node{

  def mavenHome= tool name: "maven3.9.6"

  try{
    sendslacknotifications("STARTED")

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

}//try closing
catch(e){
  currentBuild.result= "FAILURE"
}//catch block closing
finally{
  sendslacknotifications(currentBuild.result)
}//finally closing

}//node closing


def sendslacknotifications(String buildStatus = 'STARTED') {
  // build status of null means successful
  buildStatus =  buildStatus ?: 'SUCCESSFUL'

  // Default values
  def colorName = 'RED'
  def colorCode = '#FF0000'
  def subject = "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
  def summary = "${subject} (${env.BUILD_URL})"

  // Override default values based on build status
  if (buildStatus == 'STARTED') {
    colorName = 'YELLOW'
    colorCode = '#FFFF00'
  } else if (buildStatus == 'SUCCESSFUL') {
    colorName = 'GREEN'
    colorCode = '#00FF00'
  } else {
    colorName = 'RED'
    colorCode = '#FF0000'
  }

  // Send notifications
  slackSend (color: colorCode, message: summary, channel: #walmart-dev)
}
