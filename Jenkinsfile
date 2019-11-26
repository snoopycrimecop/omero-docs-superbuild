pipeline {
    agent {
        label 'testintegration'
    }

    environment {
        // Default credentials for testing on devspace
        MAVEN_SNAPSHOTS_REPO_URL = 'http://nexus:8081/nexus/repository/maven-internal/'
        MAVEN_USER = 'admin'
        MAVEN_PASSWORD = 'admin123'

        // Disable Gradle daemon
        GRADLE_OPTS = '-Dorg.gradle.daemon=false'
    }

    stages {
        stage('Versions') {
            steps {
                sh 'echo Disable versions copy until needed'
            }
        }
        stage('Build') {
            steps {
                sh """
                    cd ${env.WORKSPACE}/ome-documentation
                    ./autogen_omero.sh
                """
                archiveArtifacts artifacts: '*/dist/*tar.gz'
            }
        }
        stage('Deploy') {
            steps {
                sh 'echo see https://help.sonatype.com/repomanager3/formats/pypi-repositories'
                sh 'echo was gradle --init-script init-ci.gradle publish'
            }
        }
    }

    post {
        always {
            // Cleanup workspace
            deleteDir()
        }
    }

}
