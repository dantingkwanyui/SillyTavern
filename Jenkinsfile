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
    tools { nodejs 'nodejs' }
    environment {
        FAAS_PW = credentials('openfaas-pw')
        FAAS_GATEWAY = credentials('faas-gateway')
    }
    stages {
        stage('preflight checking') {
            steps {
                echo "Hello World!!!!!!!!!!!!!!!!!${WORKSPACE}!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!"
                echo sh(returnStdout: true, script: 'env')
                sh 'node -v'
            }
        }
        stage('faas-cli'){
            steps {
                sh 'curl -sSL https://cli.openfaas.com | sh'
                sh "echo ${FAAS_PW} | ./faas-cli login -g ${FAAS_GATEWAY} --password-stdin"
                sh "cd ${WORKSPACE}/openfaas"
                sh "./faas-cli template store pull golang-middleware"
                sh './faas-cli up'
            }
        }
        stage('build') {
            steps {
                sh "cd ${WORKSPACE}"
                sh 'npm --version'
                sh 'git log --reverse -1'
                sh 'npm install'
                sh 'npm start'
            }
        }
    // stage('test') {
    //     steps {
    //         sh 'npm test'
    //     }
    // }
    }
}
