pipeline {
    agent any
    stages {
		stage ( 'Unit Test') {
            steps {
            
                sh 'ant -f test.xml -v'
				junit 'reports/result.xml'
            }
        }
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