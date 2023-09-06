pipeline { 
    agent any
    
    stages {
    
        stage("build") {
            steps {
                sh "./mvnw package"
            }
        }

        stage("Capture") {
            steps {
                archiveArtifacts '**/target/*.jar'
                jacoco()
                junit '**/target/surefire-reports/*.xml'
            }
        }
        
    }
    post {
        
        always { 
            emailext body: "$BUILD_URL\n${currentBuild.absoluteUrl}", 
                recipientProviders: [previous()], 
                subject: "${currentBuild.currentResult}: Job $JOB_NAME [$BUILD_NUMBER]", 
                to: 'always@foo.bar'
        }
        
    }
}

