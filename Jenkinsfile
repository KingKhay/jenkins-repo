pipeline{
    agent none
    environment {
        DB_ENGINE = 'sqlite'
        ADMIN_ASSIGNED = 'Khay'
    }
    stages{
        stage('Build'){
            agent {
                label 'linux'
            }
            steps{
                echo "Database Engine is ${DB_ENGINE}"
                echo "Admin Assigned is ${ADMIN_ASSIGNED}"
            }
        }
        stage('Test'){
            //If there is a dockerfile within the root of the repo the build would run in the resulting container of the dockerfile
            agent { dockerfile true}
            steps{
                sh "echo run using the dockerfile"
            }
        }
        stage('Final'){
            agent {
                dockerContainer { image 'node:18.6.0-alpine'}
            }
            steps{
                sh 'node --version'
            }
        }
    }
    post{
        always{
            echo "Pipeline Finished Running"
        }
        failure{
            echo "Failed"
        }
        success{
            echo "Successful"
        }
    }
}