pipeline {
    agent { label 'built-in' }

    environment {
        BLACK='\u001b[30m'
        RED='\u001b[31m'
        GREEN='\u001b[32m'
        END='\033[0m'
        REPOSITORY_URL='https://github.com/AndriyShkrobut/jenkins-job-builder.git'
    }

    options {
        timestamps()
        ansiColor('xterm')
    }

    stages {
        stage('Checkout') {
            steps {
                echo "${env.GREEN}Checking out Jenkins Job Builder repository${env.END}"
                checkout(
                    [$class: 'GitSCM',
                        branches: [
                            [name: 'master']
                        ],
                        extensions: [],
                        userRemoteConfigs: [
                            [url: "${env.REPOSITORY_URL}"]
                        ]
                    ]
                )
            }
        }

        stage('Build Docs') {
            steps {
                echo "${env.GREEN}Build Docs${env.END}"
                sh 'tox -e docs'
            }
        }

        stage('Build Coverage') {
            steps {
                echo "${env.GREEN}Build Coverage${env.END}"
                sh 'tox -e cover'
            }
        }
        
	stage('Build for Python 3.8') {
            steps {
                echo "${env.GREEN}Build for Python 3.8${env.END}"
                sh 'tox -e py38'
            }
        }
    }
}
