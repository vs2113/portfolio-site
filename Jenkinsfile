pipeline {
    agent any
    environment {
        GIT_CRED = 'github-pat' // The Jenkins credential ID for your Personal Access Token
        GIT_URL = 'https://github.com/vs2113/portfolio-site.git'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM',
                          branches: [[name: '*/main']],
                          userRemoteConfigs: [[
                              url: "${GIT_URL}",
                              credentialsId: "${GIT_CRED}"
                          ]]
                ])
            }
        }
        stage('Deploy to gh-pages') {
            steps {
                sh '''
                git checkout --orphan gh-pages
                git rm -rf .
                cp index.html about.html style.css .
                git add .
                git commit -m "Update site from Jenkins"
                git push origin gh-pages --force
                '''
            }
        }
    }
}
