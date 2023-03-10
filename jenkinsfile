node{
 def mavenHome = tool name: "3.8.2"
 
 echo "Git BranchName: ${env.BRANCH_NAME}" 
 echo "Jenkins Job Number: ${env.BUILD_NUMBER}"
 echo "Jenkins Node Name: ${env.NODE_NAME}"
 
 echo "Jenkins Home: ${env.JENKINS_HOME}" 
 echo "Jenkins URL: ${env.JENKINS_URL}"
 echo "JOB Name: ${env.JOB_NAME}"

 stage('checkoutcode')
 {
 git branch: 'development', credentialsId: 'a6a4aa91-6b6c-4737-a505-5c24f5e51c65', url: 'https://github.com/harika-aws/maven-web-application-2.git'
 }
 
 stage('branch')
 {
 sh "${mavenHome}/bin/mvn clean package"
 }
 stage('sonarqubereport')
 {
 sh "${mavenHome}/bin/mvn clean sonar:sonar"
 }
 stage('upload artifact into nexus')
 {
 sh "${mavenHome}/bin/mvn clean deploy"
 }
 stage('Deployappintotomcatsever')
 {
 sshagent(['28bb91ed-4e6e-4dda-b2c9-a2dccaf20a8e']) {
 sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.211.88.44:/opt/apache-tomcat-9.0.73/webapps/"
}
 }
 stage('sendEmailnotification')
 {
 emailext body: '''build is over!!
     

Regards
harika ummidi
''', subject: 'build over!!', to: 'harikaummidisoc@gmail.com'
 }
} 
 













