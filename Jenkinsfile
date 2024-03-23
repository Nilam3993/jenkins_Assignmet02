pipeline {
    agent any
    stages {
        stage('Docker Image Build IN Dev') {
            when {
                branch 'dev'
            }
            steps {
                script {
                    def app = docker.build("nilamballal169/dev:latest")
                    docker.withRegistry('https://registry.hub.docker.com', 'docker_cred') {
                        app.push()
                    }
                }
            }
        }
        stage('Build Docker QA Image') {
            when {
                branch 'qa'
            }
            steps {
                script {
                    def app = docker.build("nilamballal169/qa:latest")
                    docker.withRegistry('https://registry.hub.docker.com', 'docker_cred') {
                        app.push()
                    }
                }
            }
        }
    }
    post { 
        always { 
            echo 'Deleting Project now !! '
            deleteDir()
        }
    }
}
