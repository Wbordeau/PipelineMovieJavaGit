pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M3"
        jdk "JDK11"
    }

    stages {
	
        stage('Compile') {
            steps {
                // Get some code from a GitHub repository
                git url: 'https://github.com/mattcol/movieapijava2021.git',
                    branch: 'dev'
				// Run Maven on a Unix agent.
                sh "mvn clean compile"
            }
        }
		
        stage('Tests') {
            steps {
                // To run Maven on a Windows agent, use
                sh "mvn test"
            }
			post {
				always {
					junit '**/target/surefire-reports/TEST-*.xml'
				}
			}
        }
		
        stage('package') {
            post {
				sh "mvn -DskipTests package"

                }
            }
        }
    }
}
