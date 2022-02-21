pipeline {

    environment {
        dockerimagename = "sandipxds/nodeapp"
        dockerImage = ""
    }

    agent any

    stages {

        stage('Clone NODEAPP_Test Repo of Blazinglinux'){
            steps {
                git 'https://github.com/Blazinglinux/nodeapp_test.git'
            }
        }

        stage('Build Docker Image'){
            steps{
                script {
                    dockerImage = docker.build dockerimagename
                }
            }
        }

        stage('Docker Login') {
            steps{
                sh 'docker login -u sandipxds -p d65219d7-c503-4714-9145-51b5278fff1e'
            }
        }

        stage("Deploy App to Kubernetes"){
            steps{
                script{
                    kubernetesDeploy(configs: "deploymentservice.yml", kubeconfigId: "kubernetes")
                }
            }
        }


     }




    }
