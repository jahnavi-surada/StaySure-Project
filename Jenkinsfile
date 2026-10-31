
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Generate Prisma Client') {
            steps {
                bat 'npx prisma generate'
            }
        }

        stage('Database Migration') {
            steps {
                bat 'npx prisma migrate deploy'
            }
        }

        stage('Build') {
            steps {
                bat 'npm run build'
            }
        }

        stage('Test') {
            steps {
                bat '''
                if not exist .next\\BUILD_ID (
                    echo Build verification failed!
                    exit /b 1
                )
                echo Build verification successful!
                '''
            }
        }
    }
	stage('Deploy') {
	    steps {
        	bat 'kubectl apply -f deployment.yaml'
        	bat 'kubectl apply -f service.yaml'
        	bat 'kubectl rollout status deployment/staysure-deployment --timeout=120s'
	    	}
	}

    post {
        success {
            echo 'StaySure pipeline completed successfully!'
        }
        failure {
            echo 'StaySure pipeline failed. Check the console output.'
        }
        always {
            echo 'Pipeline execution finished.'
        }
    }
}
