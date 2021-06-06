node{
    def mavenHome = tool name: 'maven3.8.1'
  stage('CodeClone') {
    git credentialsId: 'GitHub', url: 'https://github.com/Sheckle/web.git'
  }
  stage('mavenBuild') {
    sh "${mavenHome}/bin/mvn clean package"
  }
   stage('CodeQuality') {
    sh "${mavenHome}/bin/mvn sonar:sonar"
  }
    stage('emailDeployIssues') {
  emailext body: '''project successful
Don''', recipientProviders: [developers()], subject: 'build status', to: 'shackle_d@yahoo.com'
  }
  stage('UploadNexus') {
    sh "${mavenHome}/bin/mvn deploy"
  }
  stage('DeployTomcat') {
      deploy adapters: [tomcat9(credentialsId: 'tomcat2', path: '', url: 'http://18.191.156.2:8080')], contextPath: null, war: 'target/*war'
  }
  stage('emailDeployIssues') {
  emailext body: '''project successful
Don''', recipientProviders: [developers()], subject: 'build status', to: 'shackle_d@yahoo.com'
  }
  }
