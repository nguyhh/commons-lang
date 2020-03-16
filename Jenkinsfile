def STABLE = '94b3784fdec5d0e9d63e4aec6772144b68283790'
def BROKEN = '46578439ab651402b8bde0cba09a877f63ac7eaf'

pipeline{
    agent any
    stages{
        stage('Build'){
            steps{
                sh'mvn clean compile test -Drat.numUnapprovedLicenses=10'
            }
        }

    }
    post{
        success{
            mail to: 'nguyenhaiha1224@gmail.com',
            subject: "Sucess Pipeline: ${currentBuild.fullDisplayName}",
            body: "Build success ${env.BUILD_URL}"

        }
        failure {
            sh "git bisect start ${BROKEN} ${STABLE}"
		    sh "git bisect run mvn clean test"
		    sh "git bisect log>bisect.log"
		    sh "git bisect reset" 

        }
    }
    
}