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
                 sh 'curl -uadmin:AP7GYRXDfu6Q6VZCmgkygxJjAZ4 -T /home/jenkins/node/workspace/Mule_CICD_Abhishek/target/test1-1.0.0-SNAPSHOT-mule-application.jar "http://mdcassimsait.southindia.cloudapp.azure.com:8081/artifactory/example-repo-local/$BUILD_NUMBER/test1-1.0.0-SNAPSHOT-mule-application.jar"'
			}
        }
		stage('Deploy CloudHub') { 
			//environment {
			//	ANYPOINT_CREDENTIALS = credentials('anypoint.credentials')
			//}
			steps {
				sh 'curl -uadmin:AP7GYRXDfu6Q6VZCmgkygxJjAZ4 -O "http://mdcassimsait.southindia.cloudapp.azure.com:8081/artifactory/example-repo-local/$BUILD_NUMBER/test1-1.0.0-SNAPSHOT-mule-application.jar"'
				sh 'mvn clean deploy -P cloudhub -Dmule.version=3.9.0 -Danypoint.username=ankitshastri05 -Danypoint.password=Ashu52824@'
				}
		}
    }
}
