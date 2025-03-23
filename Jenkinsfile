pipeline {
    agent any
    stages {
	stage('docker run base') {
            steps {
                sh 'sudo docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=Qwerty-1" -p 1433:1433 --name sql111 --hostname sql1 -d mcr.microsoft.com/mssql/server:2022-latest'
            }
        }
	stage('Docker-build-bek') {
            steps {
                sh 'sudo docker build -t bek /var/lib/jenkins/workspace/site/BackEnd/Amazon-clone/'
            }
        }
        stage('docker run bek') {
            steps {
                sh 'sudo docker run -d -p 5034:5034 bek'
            }
        }
        stage('Docker-build-front') {
            steps {
                sh 'sudo docker build -t front /var/lib/jenkins/workspace/site/FrontEnd/my-app/'
            }
        }
        stage('docker run front') {
            steps {
                sh 'sudo docker run -d -p 81:80 front'
            }
        }
    }
}
