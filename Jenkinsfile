pipeline {
    agent any
    stages {
stage('Build') {
	steps {
		echo "RunningBuild automation"
		sh './gradlew build --no-deamon'
		archiveArtifacts artifacts: 'dist/trainSchedule.zip'
		}
	}
stage('Build Docker image') {
	when {
  		branch 'master'
		}

	steps{
	script {
		app = docker.build("DockerHub>/node-app")
		app.inside {
			sh 'echo $(curl localhost:8080)'
			}
			}
		}
	}
stage('push docker image')
	{
	when {
		branch 'master'
		}
	steps {
		script {
			docker.withRegistry('https://registry.hub.docker.com','DockerHub')
			{
				app.push("${env.BUILD_NUMBER}")
				app.push("latest")
			}
		}
	}
	}
           }
}
