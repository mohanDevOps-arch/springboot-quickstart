pipeline {
    agent any

    tools {
        maven 'Maven 3'    // Define this in Jenkins Global Tool Config
        jdk 'JDK 17'       // Also define in Global Tool Config
    }

    stages {
        stage('Clone') {
            steps {
                git 'pipeline {
    agent any

    tools {
        maven 'Maven 3'    // Define this in Jenkins Global Tool Config
        jdk 'JDK 17'       // Also define in Global Tool Config
    }

    stages {
        stage('Clone') {
            steps {
                git 'pipeline {
    agent any

    tools {
        maven 'Maven 3'    // Define this in Jenkins Global Tool Config
        jdk 'JDK 17'       // Also define in Global Tool Config
    }

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/samruddhibhoyar3/springboot-quickstart.git'
            }
        }

        stage('Build') {
            steps {
                echo '🔨 Building the Spring Boot app...'
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                echo '🧪 Running unit tests...'
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                echo '🚀 Deploying...'
                sh 'nohup java -jar target/*.jar &'
            }
        }
    }

    post {
        success {
            mail to: 'your-email@example.com',
                 subject: '✅ Spring Boot Build Success',
                 body: 'The Jenkins pipeline ran successfully.'
        }
        failure {
            mail to: 'your-email@example.com',
                 subject: '❌ Spring Boot Build Failed',
                 body: 'The Jenkins pipeline failed. Check console output.'
        }
    }
}
'
            }
        }

        stage('Build') {
            steps {
                echo '🔨 Building the Spring Boot app...'
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                echo '🧪 Running unit tests...'
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                echo '🚀 Deploying...'
                sh 'nohup java -jar target/*.jar &'
            }
        }
    }

    post {
        success {
            mail to: 'your-email@example.com',
                 subject: '✅ Spring Boot Build Success',
                 body: 'The Jenkins pipeline ran successfully.'
        }
        failure {
            mail to: 'your-email@example.com',
                 subject: '❌ Spring Boot Build Failed',
                 body: 'The Jenkins pipeline failed. Check console output.'
        }
    }
}
'
            }
        }

        stage('Build') {
            steps {
                echo '🔨 Building the Spring Boot app...'
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                echo '🧪 Running unit tests...'
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                echo '🚀 Deploying...'
                sh 'nohup java -jar target/*.jar &'
            }
        }
    }

    post {
        success {
            mail to: 'your-email@example.com',
                 subject: '✅ Spring Boot Build Success',
                 body: 'The Jenkins pipeline ran successfully.'
        }
        failure {
            mail to: 'your-email@example.com',
                 subject: '❌ Spring Boot Build Failed',
                 body: 'The Jenkins pipeline failed. Check console output.'
        }
    }
}
