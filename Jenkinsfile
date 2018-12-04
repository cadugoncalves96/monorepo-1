#!/usr/bin/env groovy

pipeline {
    agent any
    
    stages {
        stage('init') {
            steps {
                script {
                    def scmVars = checkout scm
                    env.ULTIMO_COMMIT = scmVars.GIT_PREVIOUS_SUCCESSFUL_COMMIT
                }
            }
        }
        stage('site1') {
            when {
                expression {
                    matches = sh(returnStatus:true, script: "git diff --name-only $ULTIMO_COMMIT|egrep -q '^site1'")
                    return !matches
                }
            }
            steps {
                build 'site1'
            }
        }
        stage('site2') {
            when {
                expression {
                    matches = sh(returnStatus: true, script: "git diff --name-only $ULTIMO_COMMIT|egrep -q '^site2'")
                    return !matches
                }
            }
            steps {
                build 'site2'
            }
        }
    }
}
