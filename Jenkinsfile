pipeline {
    agent any

    environment {
        PORT = 80

        IMAGE_NAME = 'nginx-image'
        CONT_NAME = 'nginx-cont'

        home_service_url            = 'http://localhost:3000'
        payments_service_url        = 'http://localhost:3003'
        messages_service_url        = 'http://localhost:3001'
        nav_service_url             = 'http://localhost:3002'
        sponsors_list_service_url   = 'http://localhost:3005'
        search_service_url          = 'http://localhost:3004'
    }

    stages {
        stage('Build') {
            steps {
                sh 'docker build -t ${IMAGE_NAME}  .'
            }
        }
        stage('Run') {
            steps {
                sh 'docker rm -f ${CONT_NAME}'
                sh 'docker run --name ${CONT_NAME} -d -p ${PORT}:80 --env-file <<< "$(env | grep "_service_url$")" ${IMAGE_NAME}' 
            }
        }
    }
}
