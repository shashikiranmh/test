pipeline {
    agent {
        node {
            label 'maven'
        }
    }
environment {
    PATH = "/opt/apache-maven-3.9.4/bin:$PATH"
}
    stages {
        stage('bulid-java') {
            steps {
                sh 'mvn clean deploy -Dmaven.unit-test.skip=true'
            }
        }

    stage("unit-test"){
            steps{
                echo "----------- unit test started ----------"
                sh 'mvn surefire-report:report'
                 echo "----------- unit test Complted ----------"
            }
        }
    
   stage('SonarQube analysis') {
    environment {
       scannerHome = tool 'dev-sonarqube-scanner'
    }
    steps {
    withSonarQubeEnv('dev-sonar-server') { // If you have configured more than one global server connection, you can specify its name
      sh "${scannerHome}/bin/sonar-scanner"
    }
    }
   }
  }
}

