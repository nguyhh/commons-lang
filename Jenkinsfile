def STABLE = '94b3784fdec5d0e9d63e4aec6772144b68283790'
def BROKEN = '899e92684c5d620567fdf4c45c7c51a5426a8aeb'
pipeline{
    agent any
    stages{
        stage('Build'){
            steps{
                sh'mvn clean test -Drat.numUnapprovedLicenses=10'
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
		    sh "git bisect run mvn clean test -Drat.numUnapprovedLicenses=10"
		    sh "git bisect log>bisect.log"
		    sh "git bisect reset" 

        }
    }
    
}