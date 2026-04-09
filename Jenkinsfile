pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/madhan-231105/sample-project.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                python -m venv venv
                source venv/bin/activate
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                source venv/bin/activate
                PYTHONPATH=. pytest
                '''
            }
        }

stage('SonarQube Analysis') {
    steps {
        withSonarQubeEnv('My Sonar Server') {
            script {
                def scannerHome = tool 'SonarScanner'
                sh """
                source venv/bin/activate
                ${scannerHome}/bin/sonar-scanner
                """
            }
        }
    }
}

// stage('Quality Gate') {
//     steps {
//         timeout(time: 5, unit: 'MINUTES') {
//             waitForQualityGate abortPipeline: true
//         }
//     }
// }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t myapp:latest .'
            }
        }
    }
}