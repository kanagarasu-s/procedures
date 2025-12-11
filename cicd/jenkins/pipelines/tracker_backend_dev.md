pipeline {
    agent any

    environment {
        
        WORKDIR = '/var/www/html/staging/tracker-backend-v2'
        GIT_CREDENTIALS_ID = 'github-cred'
    }
    
    //triggers {
    //pollSCM('* * * * *') 
    //}

    stages {
        stage('Git Checkout DEV Branch') {
            steps {
                sh 'pwd'
                git branch: 'dev',
                    credentialsId: 'github-cred', 
                    url: 'https://github.com/SQ1Security/tracker-backend-v2.git'
            }
        }
        stage('Git Pull Dev Branch') {
            steps {
                withCredentials([usernamePassword(credentialsId: env.GIT_CREDENTIALS_ID, usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD')]) {
                    sh '''
                        cd ${WORKDIR}
                         git config --global --add safe.directory ${WORKDIR}
                         git pull https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/SQ1Security/tracker-backend-v2.git dev
                    '''
                }
            }
        }
        
        stage('Composer Update') {
            steps {
                dir("${WORKDIR}") {
                    sh 'composer update'
                }
            }
        }

        stage('Run Migrations') {
            steps {
                dir("${WORKDIR}") {
                    sh 'php artisan migrate'
                }
            }
        }

        stage('Run Optimize Clear') {
            steps {
                dir("${WORKDIR}") {
                    sh 'php artisan optimize:clear'
                }
            }
        }
    }
}
