pipeline {
    agent any

    environment {
        PORT = 80
        NETWORK = "mf-net"

        IMAGE_NAME = 'nginx-img'
        CONT_NAME = 'nginx'

        main_service_url            = 'http://mf-main/'
        payments_service_url        = 'http://mf-payments/'
        cards_service_url           = 'http://mf-cards/'
        navigation_service_url      = 'http://mf-navigation/'
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
                sh 'docker run -d \
                    --name ${CONT_NAME} \
                    --net ${NETWORK} \
                    -p ${PORT}:${PORT} \
                    -e PORT=${PORT} \
                    -e main_service_url=${main_service_url} \
                    -e payments_service_url=${payments_service_url} \
                    -e cards_service_url=${cards_service_url} \
                    -e navigation_service_url=${navigation_service_url} \
                    ${IMAGE_NAME}' 
            }
        }
    }
}
