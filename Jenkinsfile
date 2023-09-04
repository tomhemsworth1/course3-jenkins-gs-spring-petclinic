pipeline { 
    agent any
    
    stages {
    
        stage("checkout") {
            steps {
                git branch: 'main', url: "https://github.com/tomhemsworth1/course3-jenkins-gs-spring-petclinic.git"
            }
        }
        
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

