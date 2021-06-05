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
        dashboard_service_url       = 'http://localhost:5000'
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
                sh 'docker run \
                    --name ${CONT_NAME} \
                    -d \
                    -p ${PORT}:80 \
                    -e home_service_url=${home_service_url} \
                    -e payments_service_url=${payments_service_url} \
                    -e messages_service_url=${messages_service_url} \
                    -e nav_service_url=${nav_service_url} \
                    -e sponsors_list_service_url=${sponsors_list_service_url} \
                    -e search_service_url=${search_service_url} \
                    ${IMAGE_NAME}' 
            }
        }
    }
}
