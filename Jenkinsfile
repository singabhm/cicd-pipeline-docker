pipeline {
    agent any
    stages {
stage('Build') {
	steps {
		echo "RunningBuild automation"
		sh './gradlev build --no-deamon'
		archiveArtifacts artifacts: 'dist/trainSchedule.zip'
	}
	}
stage('Build Docker image') {
when {
  branch 'master'
}

	steps{
	script {
		app = docker.build("docker_logi_id>/node-app")
		app.inside {
			sh 'echo $(curl localhost:8081)'
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
		docker.withRegistry("https://registry.hub.docker.com', 'docker_hub_login') {
		app.push("${env.BUILD_NUMBER}")
		app.push("latest")
}
}
}
}
                            }
}
