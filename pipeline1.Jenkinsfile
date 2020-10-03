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
                    log.info("The current build number is " + buildNumber)
                    log.warning("The current build number is " + buildNumber)
                    log.error("The current build number is " + buildNumber)
				}
			}
		}
        stage("Build"){
            steps {
				script {
					echo "Build stage"
                    def buildUser = sh(script: 'id', returnStdout: true)
                    log.info("building os user is " + buildUser)

                    buildStageReturn = sh(script: 'pwd', returnStatus: true)
					log.info("return code is " + buildStageReturn)
				}
            }
        }
        stage("Test"){
			when {
                expression {
                    buildStageReturn == "0" //run if build stage succeeded
                }
            }
            steps {
				echo "Build Sucess! Start Test Stage"
                echo "Testing"
            }
        }
        stage("End"){
            steps {
                echo "End Stage"
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

