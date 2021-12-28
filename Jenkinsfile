pipeline {
    environment {
        registry = "bbumba/bootcamp"
        registryCredential = '795d7a3c-4d21-4e7a-abc6-aaeb6ee8ae6e'
        dockerImage = ''
    }
    agent any
    stages {
        stage('Cloning our Git') {
            steps {
                git 'https://github.com/BOsmola/practice.git'
            }
        }
        stage('Building our image') {
            steps{
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Deploy our image') {
            steps{
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage("3"){
            steps{
                sh "kubectl create deployment practice --image=bbumba/practice:$BUILD_NUMBER-1"
            }
        }
        stage('Cleaning up') {
            steps{
                sh "docker rmi $registry:$BUILD_NUMBER"
            }
        }
    }
}
