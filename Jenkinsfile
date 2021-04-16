pipeline {
    agent {
    	docker {
            image 'maven:3.6.3-jdk-11' 
            args '-v $HOME/.m2:/root/.m2' 
        }
    }
    parameters {
        string(name: 'ReleaseVersion', defaultValue: '1.0', description: 'Release version')
        string(name: 'DevVersion', defaultValue: '1.1', description: 'Dev version')
    }
    stages {
        stage('Build') { 
            steps {
                sh "mvn -B -DskipTests clean package" 
            }
        }
        stage("Release") {
        	steps {
				sh "release:prepare -DreleaseVersion=${params.ReleaseVersion} -DdevelopmentVersion=${params.DevVersion}-SNAPSHOT"
				sh "mvn release:perform"
            }
        }
    }
}