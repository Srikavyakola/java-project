pipeline {
    agent {
        label 'master'
    }
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
        stage ( 'Deploy') {
            steps {
                sh "cp dist/rectangle_${env.BUILD_NUMBER}.jar /var/www/html/rectangles/all"
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'dist/*.jar', fingerprint: true

        }

    }
}