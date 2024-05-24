// this is th jenkins file for my new pipeline demo 
// i am learning the jenkins by writing declarative pipeline instead of scripted pipeline

pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo " this is nischal chudal"
                input("do you want to continue ")
            }
        }
        stage('Test') {
            steps {
                echo " this is the second stage  name test"
            }
        }
        stage('Deploy') {
            steps {
                echo " this is the deploy stage where i will deploy the code to the git after it is tested"
            }
        }
    }
}
