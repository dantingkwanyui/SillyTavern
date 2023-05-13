/* groovylint-disable LineLength */
/* groovylint-disable-next-line CompileStatic */
pipeline {
    // agent {
    //     kubernetes {
    //         inheritFrom 'slave'
    //     }
    // }
    agent {
        kubernetes {
            label 'slave'
        }
    }
    tools {
        nodejs 'nodejs'
    }
    environment {
        OPENFAAS_PASSWORD = credentials('OPENFAAS_PASSWORD')
        OPENFAAS_URL = credentials('OPENFAAS_URL')
        OPENFAAS_PATH = "${WORKSPACE}/openfaas"
        HARBOR_DOCKER_HOST = credentials('HARBOR_DOCKER_HOST')
        HARBOR_DOCKER_USER = credentials('HARBOR_DOCKER_USER')
        HARBOR_DOCKER_PASSWORD = credentials('HARBOR_DOCKER_PASSWORD')
    }
    stages {
        stage('Openfaas') {
            steps {
                container('dind') {
                    sh """
                                apk add curl git
                                curl -sSL https://cli.openfaas.com | sh
                                docker login --username=${HARBOR_DOCKER_USER} --password=${HARBOR_DOCKER_PASSWORD} ${HARBOR_DOCKER_HOST}
                                cd ${OPENFAAS_PATH}
                                faas-cli template store pull golang-middleware
                                faas-cli login -g ${OPENFAAS_URL} -u admin -p ${OPENFAAS_PASSWORD}
                                faas-cli up
                    """
                }
            }
        }
        stage('Nodejs') {
            steps {
                sh '''
                    node -v'
                    npm --version
                    git log --reverse -1
                    npm install
                    npm start
                '''
            }
        }
    }
}
