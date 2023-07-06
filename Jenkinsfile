pipeline {
    agent any
    stages {
        stage("Clone Source") {
            steps {
                echo 'Clone Source'
                git branch: 'master', url: 'git@github.com:stevanojsuwuh/robot-jenkins-with-docker.git'
            }
        }

        stage("Robot Test") {
            steps {
                echo 'Robot Test'
                sh '/home/enigma/anaconda3/bin/robot -d Results main.robot'
            }
        }
    }
    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
            slackSend(channel: '#training', message: "Build deployed successfully - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)")
        }
        failure {
            echo 'This will run only if failed'
            slackSend(channel: '#training', message: "Build deployed failed - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)")
        }
    }
}