pipeline {
    agent any
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
        		sh '''
                git config user.email "remy.girodon@gmail.com"
                git config user.name "rgirodon"
                '''
                sh "mvn -B release:clean"
				sh "mvn -B release:prepare -DreleaseVersion=${params.ReleaseVersion} -DdevelopmentVersion=${params.DevVersion}-SNAPSHOT"
				sh "mvn -B release:perform"
            }
        }
    }
}