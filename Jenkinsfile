pipeline {
	environment {
		MAJOR_VERSION = 1
	}
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
				
                sh "cp dist/rectangle_${env.MAJOR_VERSION}.${env.BUILD_NUMBER}.jar /var/www/html/rectangles/all/${env.BRANCH_NAME}/"
            }
        }
		
		stage ( 'Functional testing') {
			steps {
				sh "wget http://srikavyakola3.mylabserver.com/rectangles/all/${env.BRANCH_NAME}/rectangle_${env.MAJOR_VERSION}.${env.BUILD_NUMBER}.jar"
				sh "java -jar rectangle_${env.MAJOR_VERSION}.${env.BUILD_NUMBER}.jar 4 5"
			}
		}
		stage ( 'Promote to green') {
			when {
				branch 'master'
			}
			steps {
				sh "cp /var/www/html/rectangles/all/rectangle_${env.MAJOR_VERSION}.${env.BUILD_NUMBER}.jar /var/www/html/rectangles/green/rectangle_${env.MAJOR_VERSION}.${env.BUILD_NUMBER}.jar"
			}
		
		}
		stage ('Promoting development branch to master') {
			when {
				branch 'development'
			}
			steps {
				sh 'git checkout development'
				sh 'git pull'
				echo "checking out master branch"
				sh 'git checkout master'
				echo "merging development into master"
				sh 'git merge development'
				echo "pushing to origin master"
				sh 'git push origin master'
				echo "tagging to release"
				sh "git tag rectangle-${env.MAJOR_VERSION}.${env.BUILD_NUMBER}"
				sh "git push origin rectangle-${env.MAJOR_VERSION}.${env.BUILD_NUMBER}"
			}
		}
	}
}






















