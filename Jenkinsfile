pipeline {
    agent any
    
    environment {
        SONAR_TOKEN = credentials('sonarToken')
    }
    
    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning repository...'
                git branch: 'main',
                    url: 'https://github.com/medaminejendoubi07/DevOps'
            }
        }
        
        stage('Build with Maven') {
            steps {
                echo 'Building the project with Maven...'
                sh 'mvn clean install'
            }
        }
        
        stage('SonarQube Analysis') {
            steps {
                echo 'Analyzing code quality with SonarQube...'
                sh """
                    mvn sonar:sonar \\
                    -Dsonar.host.url=http://192.168.33.10:9000 \\
                    -Dsonar.token=\${SONAR_TOKEN}
                """
            }
        }
        
        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t medaminejendoubi07/springboot:${BUILD_NUMBER} .'
            }
        }
    }
}
