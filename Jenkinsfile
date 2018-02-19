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
                
                sh 'ant -f build.xml -v'
				
            }
			post {
				success {
					archiveArtifacts artifacts: 'dist/*.jar', fingerprint: true
				}

			}
        }
		
		stage ( 'Deploy') {
            steps {
                sh "cp dist/rectangle_${env.BUILD_NUMBER}.jar /var/www/html/rectangles/all"
            }
        }
		
		stage ( 'Functional testing'){
			steps {
				sh "wget http://srikavyakola3.mylabserver.com/rectangles/all/rectangle_${env.BUILD_NUMBER}.jar"
				sh "java -jar rectangle_${env.BUILD_NUMBER}.jar 4 5"
			}
		}
		stage ( 'Promote to gree') {
			when {
				branch 'master'
			}
			steps {
				sh "cp /var/www/html/rectangles/all/rectangle_${env.BUILD_NUMBER}.jar /var/www/html/rectangles/green/rectangle_${env.BUILD_NUMBER}.jar"
			}
		
		}
	}
}