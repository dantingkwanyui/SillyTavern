/* groovylint-disable-next-line CompileStatic */
pipeline {
    agent {
        kubernetes {
        label 'jenkins-python'
        }
    }
    tools { nodejs 'nodejs' }
    stages {
        stage('preflight') {
            steps {
                echo 'Hello World~!!!!!!!!!!!!on!!!!!!!!!!!!'
                echo sh(returnStdout: true, script: 'env')
                sh 'node -v'
            }
        }
        stage('build') {
            steps {
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
