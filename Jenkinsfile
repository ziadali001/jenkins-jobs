#!/usr/bin/env groovy

library identifier: 'library-jenkins@master', retriever: modernSCM(
        [$class: 'GitSCMSource',
         remote: 'https://github.com/ziadali001/library-jenkins.git',
         credentialsId: 'github-credentials'
        ]
)


def gv

pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        stage("init") {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }
        stage("build jar") {
            steps {
                script {
                    buildJar()
                }
            }
        }
        stage("build and push image") {
            steps {
                script {
                    buildImage 'ziadmali/my-repo:jma-4.0'
                    dockerLogin()
                    dockerPush 'ziadmali/my-repo:jma-4.0'
                }
            }
        }
        stage("deploy") {
            steps {
                script {
                    gv.deployApp()
                }
            }
        }
    }   
}
