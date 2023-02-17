#!/usr/bin/env groovy
pipeline {
    agent {
        node any
    }

        stages {
          stage('pull-code') { 
            steps {
                git branch: 'main', credentialsId: 'enkins', url: 'https://github.com/sumit123-456/assesment.git'
            }
          }
        stage('Build') { 
            steps {
             sh 'docker build -t knx1:$BUILD_NUMBER .'
            }
        }
        stage('push') { 
            steps {
              sh 'docker tag knx1:$BUILD_NUMBER sumitperkunde/knx1:$BUILD_NUMBER'
              sh 'sudo chmod 666 /var/run/docker.sock'
              sh 'cat password.txt | docker login --username sumitperkunde --password-stdin'
              sh'docker push sumitperkunde/knx1:$BUILD_NUMBER'
            }
        }
        stage('pull & deploy') { 
            steps {
             
              sh'docker pull sumitperkunde/knx1:$BUILD_NUMBER'
              sh'docker run -itd -p 80:80 sumitperkunde/knx1:$BUILD_NUMBER'

            }
        }
    }
}
