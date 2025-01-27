pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/thesumitgogia/jenkins-learning.git' 
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    // For Angular
                    dir('frontend') {
                        sh 'npm install'
                    }

                    // For NestJS
                    dir('backend') {
                        sh 'npm install'
                    }
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    // Build Angular frontend
                    dir('frontend') {
                        sh 'ng build --prod'
                    }

                    // Build NestJS backend
                    dir('backend') {
                        sh 'npm run build'
                    }
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Run Angular unit tests
                    dir('frontend') {
                        sh 'ng test --watch=false'
                    }

                    // Run NestJS unit tests
                    dir('backend') {
                        sh 'npm run test'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Example deployment commands (adjust based on your environment)
                    dir('frontend') {
                        sh 'aws s3 sync dist/ s3://my-angular-bucket'
                    }

                    dir('backend') {
                        sh 'docker build -t my-nestjs-app . && docker run -d my-nestjs-app'
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
