pipeline {
    agent any
    environment {
        GIT_URL = 'git@github.com:stevanojsuwuh/robot-jenkins-with-docker.git'
        BRANCH = 'master'
        ROBOT = '/home/enigma/anaconda3/bin/robot'
        CHANNEL = '#training'
        IMAGE = 'my-robot-test'
        CONTAINER = 'my-robot-test-app'
        DOCKER_APP = '/usr/bin/docker'
    }
    stages {
        stage("Cleaning up") {
            steps {
                echo 'Cleaning up'
                sh "${DOCKER_APP} rm -f ${CONTAINER} || true"
            }
        }

        stage("Clone") {
            steps {
                echo 'Clone'
                git branch: "${BRANCH}", url: "${GIT_URL}"
            }
        }

        stage("Build") {
            steps {
                echo 'Build'
                sh "${DOCKER_APP} build -t ${IMAGE} ."
            }
        }

        stage("Run") {
            steps {
                echo 'Run Test'
                sh "${DOCKER_APP} run --rm ${IMAGE}"
            }
        }
    }
    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
            slackSend(channel: "${CHANNEL}", message: "Build deployed successfully - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)")
        }
        failure {
            echo 'This will run only if failed'
            slackSend(channel: "${CHANNEL}", message: "Build deployed failed - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)")
        }
    }
}