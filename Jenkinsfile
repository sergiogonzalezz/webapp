pipeline {
  agent any 
  tools {
    maven 'Maven'
  }
  stages {
    stage ('Initialize') {
      steps {
        sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
            ''' 
      }
    }
    
    stage ('Build') {
      steps {
      sh 'mvn clean package'
       }
    }
  
    stage ('Deploy-To-Tomcat') {
      steps {
        sshagent(['tomcat']) {
                sh 'scp -v -o StrictHostKeyChecking=no target/*.war ubuntu@192.168.0.19:/opt/apache-tomcat-10.0.27/webapps/webapp.war'
        }      
      }       
    }
  }
}
