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
    stages {
        stage('preflight checking') {
            steps {
                echo 'Hello World!!!!!!!!!!!!!!${WORKSPACE}!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!'
                echo sh(returnStdout: true, script: 'env')
                sh 'node -v'
            }
        }
        stage('install faas-cli'){
            sh 'curl -sSL https://cli.openfaas.com | sudo sh'
                withCredentials([string(credentialsId: 'openfaas-pw', variable: 'SECRET')]) { //set SECRET with the credential content
                echo "My secret text is '${SECRET}'"
                    sh 'export PASSWORD=${SECRET}'
            }
            sh 'echo $PASSWORD | faas-cli login --password-stdin'
        }
        stage('faas-cli deploy stage'){
            sh 'cd ${WORKSPACE}'
            sh 'faas-cli up'
        }
        stage('build') {
            steps {
                sh 'cd ${WORKSPACE}'
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
