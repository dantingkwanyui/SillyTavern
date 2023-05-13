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
                                echo ncJ2w9OdswAJ | faas-cli login -g https://gateway.on9.webredirect.org --password-stdin
                                docker login --username=${HARBOR_DOCKER_USER} --password=${HARBOR_DOCKER_PASSWORD} ${HARBOR_DOCKER_HOST}
                                cd ${OPENFAAS_PATH}
                                faas-cli template store pull golang-middleware
                                faas-cli up
                    """
                }
            }
        }
    }
// steps {
//     echo "Hello World!!!!!!!!!!!!!!!!!!${WORKSPACE}!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!"
//     echo sh(returnStdout: true, script: 'env')
//     sh 'apk add curl'
//     sh 'node -v'
//     sh "docker version"
// }
// stage('faas-cli'){
//     steps {
//         sh "cd ${FAAS_PATH}"
//         sh "echo ${FAAS_PW} | ${FAAS_PATH}/faas-cli login -g ${FAAS_GATEWAY} --password-stdin"
//         sh "${FAAS_PATH}/faas-cli template store pull golang-middleware"
//         sh "${FAAS_PATH}/faas-cli up -f ${FAAS_PATH}/stack.yml"
//     }
// }
// stage('build') {
//     steps {
//         sh "cd ${WORKSPACE}"
//         sh 'npm --version'
//         sh 'git log --reverse -1'
//         sh 'npm install'
//         sh 'npm start'
//     }
// }
// stage('test') {
//     steps {
//         sh 'npm test'
//     }
// }
}
