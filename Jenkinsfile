pipeline {
    agent any 
    
    stages {
        stage ("code") {
            steps {
                echo "cloning the code"
                git url: "https://github.com/Vishal-pixel692/django-notes-app.git" ,branch: "main"
            }
        }
        stage ("buid") {
            steps {
                echo "building the code"
                sh "docker build . -t note-app"
            }
            
        }
        stage ("push tdo docker hub") {
            steps {
                echo "pushing the image"
                withCredentials([usernamePassword(credentialsId:"Dockerhub",passwordVariable:"dockerhubPass",usernameVariable:"dockerhubUser")]){
                    sh "docker tag note-app ${env.dockerhubUser}/note-app:latest"
                    sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPass}"
                    sh "docker push ${env.dockerhubUser}/note-app:latest"
                }
            }
            
        }
        stage ("deploy") {
            steps {
                echo "deploying the contain."
                sh 'docker-compose down && docker-compose up -d'
            }
        }
        
    }
}
