pipeline {
    agent any
    
    parameters {
        choice(
            choices: ['dev', 'qa', 'prod'],
            description: 'Choose environment to deploy',
            name: 'DEPLOY_ENV'
        )
        string(
            defaultValue: '1.0',
            description: 'Version to deploy',
            name: 'VERSION'
        )
        booleanParam(
            defaultValue: true,
            description: 'Should clean workspace before build?',
            name: 'CLEAN_WORKSPACE'
        )
    }
    
    stages {
        stage('Checkout') {
            steps {
                script {
                    // Checkout your repository
                    checkout scm
                }
            }
        }
        
        stage('Build') {
            steps {
                script {
                    // Perform build steps, assuming Maven for this example
                    sh 'mvn clean package'
                }
            }
        }
        
        stage('Deploy') {
            when {
                expression {
                    params.DEPLOY_ENV == 'dev' || params.DEPLOY_ENV == 'qa' || params.DEPLOY_ENV == 'prod'
                }
            }
            steps {
                script {
                    if (params.CLEAN_WORKSPACE) {
                        // Clean workspace if specified
                        cleanWs()
                    }
                    // Deploy to specified environment
                    sh '''
                    curl -X POST \
                      http://localhost:3000/client/sendMessage/comunidadezdg \
                      -H 'accept: */*' \
                      -H 'x-api-key: comunidadezdg.com.br' \
                      -H 'Content-Type: application/json' \
                      -d '{
                        "chatId": "554384887715@c.us",
                        "chatId": "5511957740557@c.us",
                        "contentType": "string",
                        "content": "teste"
                      }'
                    '''
                }
            }
        }
    }
}
