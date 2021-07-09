pipeline{
    agent any

    stages{
        stage( 'Checkout SCM'){
            steps{
                checkout scm
            }
        }
        stage('Build FrontEnd of an application'){
            agent {
                docker { 
                    image 'node:current-alpine3.13'
                    args '-v $HOME/.m2:/root/.m2'
                    }
            }

            steps{
                sh 'npm install'
                sh 'npm build'
            }

        }
        stage('Build BackEnd'){
            agent{
                    docker {
                        image 'maven:3.6.3-adoptopenjdk-8'
                        args '-v $HOME/.m2:/root/.m2'
                        }
                }
            steps{
                sh 'mvn package'
                archiveArtifacts artifacts: 'target/*.war', followSymlinks: false
            }
            
        }

    }
}
