pipeline {
    agent any
    stages {
        stage('code') {
            steps {
                git url: 'https://github.com/AshishPardikar1995/two-tier-flask-app.git', branch: 'master'
            }
        }

        stage('build') {
            steps {
                sh 'docker build -t flask-app .'
            }
        }

        stage('Push to docker hub') {
            steps {
                withCredentials([usernamePassword(
    credentialsId: 'today',
    usernameVariable: 'dockerHubUser',
    passwordVariable: 'dockerHubPass'
)]) {
    sh "echo $dockerHubPass | docker login -u $dockerHubUser --password-stdin"
}

}
            
        }

        stage('Deploy') {
            steps {
                sh 'docker compose up -d --build flask-app'
            }
        }
    }
}
