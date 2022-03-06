pipeline {
	
agent any
	
	tools {
		maven "MY_MAVEN"
		jdk "MY_JAVA"
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
				dir("${WORKSPACE}/JavaBuildPipeline/my-app") {
					sh 'echo "Building Docker Image...."'
					sh 'docker build -t vasistaops/myjavaapp:${BUILD_NUMBER} .'
					sh 'echo "Docker Image built successfully...."'
				}
			}
		}
	}
}
