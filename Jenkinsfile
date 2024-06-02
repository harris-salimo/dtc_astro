pipeline {
    agent {
        label agent1
    }

    stages {
        stage('Build') {
            steps {
                sh "docker build -t harrissalimo/astro-sample ."
                withCredentials([usernamePassword(credentialsId: 'DockerHub', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
                    sh "docker login -u ${USERNAME} -p ${PASSWORD}"
                    sh "docker push harrissalimo/astro-sample"
                }
            }
        }
        stage('Deploy') {
            steps {
                sh "docker service update -d astro-sample"
            }
        }
    }
}