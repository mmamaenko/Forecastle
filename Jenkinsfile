#!/usr/bin/env groovy
@Library('github.com/stakater/fabric8-pipeline-library@master')

def versionPrefix = ""
try {
    versionPrefix = VERSION_PREFIX
} catch (Throwable e) {
    versionPrefix = "1.0"
}

def dockerVersion = "${versionPrefix}.${env.BUILD_NUMBER}"
def dockerRegistryURL = "docker.tools.stackator.com:443"

toolsNode(toolsImage: 'stakater/pipeline-tools:1.4.0') {
    container(name: 'tools') {

        stage('checkout'){
          checkout scm
        }

        stage('Canary Release') {
              def newImageName = "${dockerRegistryURL}/${env.JOB_NAME}:${dockerVersion}"

              newImageName = newImageName.toLowerCase()
              sh "docker build -t ${newImageName} ."
              sh "docker push ${newImageName}"
        }
    }
}