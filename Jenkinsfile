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
        
        
        
 #       stage('Push Image to DockerHub'){
 #           environment {
 #               registryCredentials = "dockerhublogin"
 #               }

#            steps{
#                script {
#                    docker.withRegistry( 'https://registry.hub.docker.com', registryCredentials ) {
#                        dockerImage.push("latest")
#                    }
#                }
#            }
#        }

        stage("Deploy App to Kubernetes"){
            steps{
                script{
                    kubernetesDeploy(config: "deploymentservice.yml", kubeconfigID: "kubernetes")
                }
            }
        }


     }




    }
