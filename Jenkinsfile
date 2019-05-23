pipeline {
    agent any
    stages {
        stage('compile') {
            steps {
                sh 'gcc -o my_app main.c foo.c'
            }
        }
        stage('build') {
            steps {
                sh './my_app'
            }
        }
    }
    post {
        always {
            echo 'Build cycle successful'     
        }
    }    
}
