pipeline {
	
agent any
	
	tools {
		maven "MY_MAVEN"
		jdk "MY_JAVA"
	}

	environment {
		DOCKERHUB_CREDENTIALS = credentials('DOCKER_CREDS')
	}
	
	stages {
		//stage('Initialise') {
		//	steps {
		//		echo "PATH = ${M2_HOME}/bin:${PATH}"
		//		echo "M2_HOME = /opt/maven"
		//	}
		//}
		stage('Build Java') {
			steps {
				dir("/var/lib/jenkins/workspace/JavaBuildPipeline/my-app") {
					sh 'echo "Building JAVA Project...."'
					sh 'mvn -B -DskipTests clean package'
					sh 'echo "Jar file generated in the target folder....."'
				}
			}
		}
		stage('Build Docker Image') {
			steps {
				dir("${WORKSPACE}/my-app") {
					sh 'echo "Building Docker Image...."'
					sh 'docker build -t vasistaops/myjavaapp:${BUILD_NUMBER} .'
					sh 'echo "Docker Image built successfully...."'
				}
			}
		}
		stage('Push Docker Image') {
			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
				sh 'docker push vasistaops/myjavaapp:${BUILD_NUMBER}'
			}
		}
	}
}
