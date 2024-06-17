pipeline {
    agent any // windows agent, Jenkins-Laravel (other machine)
    
    stages {
        stage('Fetch from GitHub') { // build steps
            steps {
                echo 'Fetching from GitHub'
                git branch: 'main', url:'https://github.com/Leangkimlong/tester.git'
            }
        }
        stage('Install Composer') {
            steps {
                sh 'composer install'
            }
        }
        stage('install npm') {
            steps {
                sh 'npm i'
                sh 'npm run build'
            }
        }
        stage('Generate Key'){
            steps{
                sh 'php artisan key:generate'
            }
        }
    }
    post {
        success {
            script {
                sh 'curl -X POST -H "Content-Type: application/json" -d \'{"chat_id": "1125394926", "text": "[SUCCESS] Jenkins Build Successfully!", "disable_notification": false}\' "https://api.telegram.org/bot7111409725:AAHpjzugiaSmBHTo8dAJtTJBIfIZtsYHSUM/sendMessage"'
            }
        }
        failure{
            script {
                sh 'curl -X POST -H "Content-Type: application/json" -d \'{"chat_id": "1983989639", "text": "[FAILED] Jenkins Build Unsuccessfully! Please check jenkins for more information.", "disable_notification": false}\' "https://api.telegram.org/bot7111409725:AAHpjzugiaSmBHTo8dAJtTJBIfIZtsYHSUM/sendMessage"'
            }
        }
    }
}