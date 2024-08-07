pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                // Add your build steps here
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                // Add your test steps here
            }
        }
        stage('Deploy') {
            when {
                branch 'production'
            }
            steps {
                echo 'Deploying...'
                // Add your deploy steps here
            }
        }
    }

    post {
        success {
            script {
                if (env.BRANCH_NAME == 'development') {
                    // Merge development into staging
                    sh 'git checkout staging'
                    sh 'git merge development'
                    sh 'git push origin staging'
                } else if (env.BRANCH_NAME == 'staging') {
                    // Merge staging into production
                    sh 'git checkout production'
                    sh 'git merge staging'
                    sh 'git push origin production'
                }
            }
        }
    }
}
