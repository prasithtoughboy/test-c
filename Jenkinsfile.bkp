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
rtUpload (
    serverId: "myartifactory",
    spec:
        """{
          "files": [
            {
              "pattern": "*.c",
              "target": "generic-local/"
            }
         ]
        }"""
)
            }
        }

        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: myartifactory
                )
            }
        }
    }
}
