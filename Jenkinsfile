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
           // post { Testing
             //   always {
                   // junit 'target/surefire-reports/*.xml'
              //  }
         //   }
        }
        stage('Deliver') {
            steps {
				echo "Testing phase"
                 sh 'curl -uadmin:AP6TkAxfFF6geJ3iNAogKEYFYft -T /home/jenkins/node/workspace/Mule_CICD_Demo/target/test1-1.0.0-SNAPSHOT-mule-application.jar "http://ankitshastri05.eastus.cloudapp.azure.com:8081/artifactory/example-repo-local/$BUILD_NUMBER/test1-1.0.0-SNAPSHOT-mule-application.jar"'
			}
        }
		stage('Deploy CloudHub') { 
			//environment {
			//	ANYPOINT_CREDENTIALS = credentials('anypoint.credentials')
			//}
			steps {
				sh 'curl -uadmin:AP6TkAxfFF6geJ3iNAogKEYFYft -O "http://ankitshastri05.eastus.cloudapp.azure.com:8081/artifactory/example-repo-local/$BUILD_NUMBER/test1-1.0.0-SNAPSHOT-mule-application.jar"'
				input("Deploy Or Abort Deployment")
				sh 'mvn clean deploy -Dmule.version=4.1.4 -Danypoint.username=ankitshastri05 -Danypoint.password=Ashu52824@ -Dorg.slf4j.simpleLogger.defaultLogLevel=debug'
				}
		}
    }
}
