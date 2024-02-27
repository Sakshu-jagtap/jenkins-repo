pipeline {
    agent any
    stages {
        stage('Pull') {
            steps {
                echo "Successful pull from Git"
                git 'https://github.com/Sakshu-jagtap/jenkins-repo.git'
            }
        }
        stage('Build') {
            steps {
                echo "Building with Maven"
                sh 'mvn clean package'
            }
        }
        stage('creating tomcat image Tomcat') {
            steps {
                script {
                    sh '''cp -r /var/lib/jenkins/workspace/demo/target/*.war .
                    docker build -t  sakshijagtap457647/tomcat-1 . 
                    docker login 
                    docker push sakshijagtap457647/tomcat-1'''
                }
            }
        }
        stage('build image on k8 ') {
            steps {
                script {
                    sh 'kubectl apply -f deployment.yaml'
                }
            }
        }
        stage('getting infomation') {
            steps {
                script {
                    sh '''kubectl get pods -o wide 
                    kubectl get nodes -o wide 
                    kubectl get svc -o wide 
                    ls /var/lib/jenkins/workspace/demo/target/'''
                }
            }
        }
    }
} //update
