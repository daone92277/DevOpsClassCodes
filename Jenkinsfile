pipeline {
    agent any
    tools{
        maven 'maven'
    }
    stages {
        stage('Clone Repo') {
            steps {
                echo 'This is the clone step - step1 '
                 git 'https://github.com/daone92277/DevOpsClassCodes.git'
            }
        }
        stage('Compile') {
            steps {
                echo 'This is the compile step - step2'
               sh 'mvn compile'
            }
        }
        stage('Code Review') {
            steps {
                echo 'This is the code review step - step3'
                sh 'mvn pmd:pmd'
            }
            post{
                success{
                    recordIssues(tools:[pmdParser(pattern:'**/pmd.xml')])
                }
            }
        }
        stage('Test') {
            steps {
                echo 'This is the Testing step - step4'
                sh 'mvn test'
            }
            post{
            success{
                junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Package') {
            steps {
                echo 'This is the package step - step5'
                sh 'mvn package'
            }
            
        }
    }
}

