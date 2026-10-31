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
    }
}