pipeline{
    agent any
    stages{
        stage("code"){
            steps{
                git url: "https://github.com/manjushabhople-design/flask-app.git", branch:"master"
            }
        }
        stage("build"){
            steps{
                sh "docker build . -t flask-app "
            }
        }
        stage("push docker file"){
            steps{
                withCredentials([usernamePassword(credentialsId: 'docker-creds', passwordVariable: 'docker-pass', usernameVariable: 'docker-user')])
                    sh "docker login -u ${env.docker-user} -p ${env.docker-pass}"
                    sh "docker tag flask-app ${env.docker-user}/flask-app:latest"
                    sh "docker push ${env.docker-user}/flask-app:latest"
            }
        }
        stage("docker deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d "
            }
        }

    }

}