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
}