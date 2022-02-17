pipeline {
    agent any

    environment {
        BLACK='\u001b[30m'
        RED='\u001b[31m'
        GREEN='\u001b[32m'
        END='\033[0m'
        REPOSITORY_URL='https://github.com/AndriyShkrobut/jenkins-job-builder.git'
        COBERTURA_REPORT='cover/coverage.xml'
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
        
        stage('Build for Python 3.7') {
            agent {
                docker {
                    image 'ochirkov/jenkins_classes:py37'
                }
            }

            steps {
                echo "${env.GREEN}Build for Python 3.7${env.END}"
                sh 'tox -e py37'
            }
        }

        stage('Build for Python 3.8') {
            agent {
                docker {
                    image 'ochirkov/jenkins_classes:py38'
                }
            }

            steps {
                echo "${env.GREEN}Build for Python 3.8${env.END}"
                sh 'tox -e py38'
            }
        }
    }
}
