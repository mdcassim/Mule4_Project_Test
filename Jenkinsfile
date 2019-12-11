pipeline {
    agent {
     node { 
        label 'node1'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
		stage('SonarQube analysis') {
			steps {
				echo "SonarQube Stage"
			sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.6.0.1398:sonar'
			}
		}
        stage('Test') {
            steps {
                echo "Middle Stage"
            }
           // post {
             //   always {
                   // junit 'target/surefire-reports/*.xml'
              //  }
         //   }
        }
        stage('Deliver') {
            steps {
				echo "Testing phase"
                 sh 'curl -uadmin:AP39KsWWWRQ6hRuvygUFQuZDEYE -T /home/jenkins/node/workspace/Mule_CICD/target/maven-mule-plugin-1.10-SNAPSHOT.jar "http://mdcassimsait.southindia.cloudapp.azure.com:8081/artifactory/example-repo-local/$BUILD_NUMBER/maven-mule-plugin-1.10-SNAPSHOT.jar"'
	    }
        }
    }
}
