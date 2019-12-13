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
                 sh 'curl -uadmin:AP5r3rBQ9jvLqtQkCihjHKafUhq -T /home/jenkins/node/workspace/Mule_CICD_Abhishek/target/test1-1.0.0-SNAPSHOT-mule-application.jar "http://mdcassimsait.southindia.cloudapp.azure.com:8081/artifactory/example-repo-local/$BUILD_NUMBER/test1-1.0.0-SNAPSHOT-mule-application.jar"'
			}
        }
		stage('Deploy CloudHub') { 
			//environment {
			//	ANYPOINT_CREDENTIALS = credentials('anypoint.credentials')
			//}
			steps {
				sh 'mvn deploy:deploy-file -DgroupId=com.somecompany -DartifactId=project -Dversion=1.0.0-SNAPSHOT -DgeneratePom=true -Dpackaging=jar -DrepositoryId=jfrog -Durl=http://mdcassimsait.southindia.cloudapp.azure.com:8081/artifactory/example-repo-local -Dfile=target/test1-1.0.0-SNAPSHOT-mule-application.jar' 
			}
		}
    }
}
