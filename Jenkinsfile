pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/oussema/Devops.git'
        GIT_CREDENTIALS_ID = 'oussema-access-token' 
    }

    stages {
        stage('Load Jenkinsfile from Main') {
            steps {
                script {
                    echo 'Pulling Jenkinsfile from main branch...'
                    checkout([$class: 'GitSCM', 
                        branches: [[name: '*/main']],
                        userRemoteConfigs: [[
                            url: env.GIT_REPO,
                            credentialsId: env.GIT_CREDENTIALS_ID
                        ]]
                    ])
                }
            }
        }

        stage('Checkout and Build') {
            when {
                branch 'PR-test'
            }
            steps {
                echo 'Pulling code from PR-test branch...'
                git(
                    branch: 'PR-test',
                    url: env.GIT_REPO,
                    credentialsId: env.GIT_CREDENTIALS_ID
                )

                echo 'Building the project...'
                sh 'echo "Build process started..."'
            }
        }
    }    
}
