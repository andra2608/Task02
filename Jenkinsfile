pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Building on branch ${env.BRANCH_NAME}"
                // Add build steps here
            }
        }
        stage('Test') {
            steps {
                echo "Testing on branch ${env.BRANCH_NAME}"
                // Add test steps here
            }
        }
        stage('Deploy') {
            steps {
                script {
                    if (env.BRANCH_NAME == 'development') {
                        echo 'Deploying to development environment'
                        // Add deployment steps for development here
                    } else if (env.BRANCH_NAME == 'staging') {
                        echo 'Deploying to staging environment'
                        // Add deployment steps for staging here
                    } else if (env.BRANCH_NAME == 'production') {
                        echo 'Deploying to production environment'
                        // Add deployment steps for production here
                    }
                }
            }
        }
    }
    post {
        success {
            script {
                if (env.BRANCH_NAME == 'development') {
                    // Automatically merge changes from development to staging
                    echo 'Merging changes from development to staging'
                    sh '''
                        git config --global user.email "dileep.andra12@gmail.com"
                        git config --global user.name "andra2608"
                        git checkout staging
                        git merge development
                        git push origin staging
                    '''
                } else if (env.BRANCH_NAME == 'staging') {
                    // Automatically merge changes from staging to production
                    echo 'Merging changes from staging to production'
                    sh '''
                        git config --global user.email "dileep.andra12@gmail.com"
                        git config --global user.name "andra2608"
                        git checkout production
                        git merge staging
                        git push origin production
                    '''
                }
            }
        }
    }
}
