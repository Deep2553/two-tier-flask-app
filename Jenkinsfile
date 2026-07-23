pipeline {

    agent any

    stages {
        stage("code") {
            steps {
                git url: "https://github.com/Deep2553/two-tier-flask-app.git", branch: "main"
            }
        }

        stage("build") {
            steps {
                sh "docker build -t two-tier-flask-app ."
            }
        }

        stage("test") {
            steps {
                echo "tester ne tes case de diye...."
            }
        }

        stage("Docker hub push") {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: "dockerCred",
                    passwordVariable: "dockerHubPass",
                    usernameVariable: "dockerHubUser"
                )]) {

                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker image tag two-tier-flask-app ${env.dockerHubUser}/two-tier-flask-app:latest"
                    sh "docker push ${env.dockerHubUser}/two-tier-flask-app:latest"
                }
            }
        }

        stage("deploy") {
            steps {
                sh "docker compose up -d --build flask-app"
            }
        }
    }
}
