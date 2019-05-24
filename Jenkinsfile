pipeline {
    agent any

    stages {
        stage ('Clone') {
            steps {
                git branch: 'master', url: "https://github.com/jfrog/project-examples.git"
            }
        }

        stage ('Upload') {
            steps {
                rtUpload (
                    buildName: 'MK',
                    buildNumber: '48',
                    serverId: 'myartifactory', // Obtain an Artifactory server instance, defined in Jenkins --> Manage:
                    specPath: 'jenkins-examples/pipeline-examples/resources/props-upload.json'
                )
            }
        }

        stage ('Download') {
            steps {
                rtDownload (
                    buildName: 'MK',
                    buildNumber: '49',
                    serverId: 'myartifactory',
                    specPath: 'jenkins-examples/pipeline-examples/resources/props-download.json'
                )
            }
        }

        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    buildName: 'MK',
                    buildNumber: '48',
                    serverId: 'myartifactory'
                )

                rtPublishBuildInfo (
                    buildName: 'MK',
                    buildNumber: '49',
                    serverId: 'myartifactory'
                )
            }
        }

        stage ('Add interactive promotion') {
            steps {
                rtAddInteractivePromotion (
                    //Mandatory parameter
                    serverId: 'myartifactory',

                    //Optional parameters
                    targetRepo: 'libs-release-local',
                    displayName: 'Promote me please',
                    buildName: 'MK',
                    buildNumber: '48',
                    comment: 'this is the promotion comment',
                    sourceRepo: 'libs-snapshot-local',
                    status: 'Released',
                    includeDependencies: true,
                    failFast: true,
                    copy: true
                )

                rtAddInteractivePromotion (
                    serverId: 'myartifactory',
                    buildName: 'MK',
                    buildNumber: '49'
                )
            }
        }
    }
}
