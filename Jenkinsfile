pipeline {
    agent any
    stages {
        stage ( 'Build') {
            steps {
                echo "Testing the build stage"
                sh 'ant -f build.xml -v'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'dist/*.jar', fingerprint: true

        }

    }
}