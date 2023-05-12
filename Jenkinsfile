/* groovylint-disable-next-line CompileStatic */
pipeline {
    // options {
    //     disableConcurrentBuilds()
    // }
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
        dockerTool 'docker'
    }
    environment {
        FAAS_PW = credentials('openfaas-pw')
        FAAS_GATEWAY = credentials('faas-gateway')
        FAAS_PATH = "./openfaas"
    }
    stages {
        stage('preflight checking') {
            steps {
                echo "Hello World!!!!!!!!!!!!!!!!!${WORKSPACE}!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!"
                echo sh(returnStdout: true, script: 'env')
                sh 'node -v'
            }
        }
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
}
