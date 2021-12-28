pipeline{
    agent any
    stages{
        stage("1"){
            steps{
                sh "docker image build -f ./Dockerfile --tag $bbumba/practice ."
            }
        }
        stage("2"){
            steps{
                sh "docker image push $bbumba/practice"
            }
        }
	stage("3"){
	    steps{
		sh "kubectl create deployment practice --image=bbumba/practice"
	    }
	}
    }
}
