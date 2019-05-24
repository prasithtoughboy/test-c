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
        stage ('Configure build info') {
            steps {
rtDownload (
    serverId: "myartifactory",
    spec:
        """{
          "files": [
            {
              "pattern": "generic-local/*.h",
              "target": "/home/vvdn/Desktop/test-file"
            }
         ]
        }"""
)
            }
        }
    }
}
