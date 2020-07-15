@Library('jenkins-pipeline-lib') _

def buildStageReturn = 1

pipeline {
    agent {
        node ("master")
    }
    options {
        timestamps()
        ansiColor('xterm')
    }
    stages {
		stage("Start"){
			steps{
				script{
					def buildNumber = currentBuild.getNumber()
					echo "The current build number is ${buildNumber}"
				}
			}
		}
        stage("Build"){
            steps {
				script {
					printstring.printstring('Build stage')
					buildStageReturn = 0
					//log.info("return code is " + buildStageReturn)

				}
            }
        }
        stage("Test"){
			when {
                expression {
                    !buildStageReturn
                }
            }
            steps {
				echo "Build Sucess! Start Test stage"
                echo "Testing"
            }
        }
        stage("End"){
            steps {
                echo "Start ending stage"
            }
        }
    }
    post {
        always {
            echo "Always end"
        }
        success {
            echo 'I succeeeded'
        }
        failure {
            echo 'I failed'
        }
		cleanup {
			deleteDir()
        }
    }
}

