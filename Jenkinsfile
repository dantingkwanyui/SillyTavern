/* groovylint-disable-next-line CompileStatic */
pipeline {
    agent {
        kubernetes {
            inheritFrom 'python'
            yaml '''
apiVersion: v1
kind: Pod
metadata:
labels:
  component: ci
spec:
  # Use service account that can deploy to all namespaces
  serviceAccountName: cd-jenkins
  containers:
  - name: golang
    image: golang:1.10
    command:
    - cat
    tty: true
  - name: gcloud
    image: gcr.io/cloud-builders/gcloud
    command:
    - cat
    tty: true
  - name: kubectl
    image: gcr.io/cloud-builders/kubectl
    command:
    - cat
    tty: true
'''
        }
    }
    // agent any
    tools { nodejs 'nodejs' }
    stages {
        stage('preflight') {
            steps {
                echo 'Hello World~!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!'
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
