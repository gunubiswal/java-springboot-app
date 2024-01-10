pipeline {
    agent {
        node {
            label 'Jenkins-slave-node'
        }
    }
    environment {
        PATH = "/opt/apache-maven-3.9.6/bin:$PATH"
    }
    stages {
        stage("build"){
            steps {
                echo "build started"
                sh 'mvn clean package -Dmaven.test.skip=true'
                echo "--build completed--"
            }
        }
        stage('SonarQube analysis') {
            environment {
                scannerHome = tool 'sonar-scanner-meportal'
            }
            steps{
                withSonarQubeEnv('sonar-server-meportal') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }



    }
}
