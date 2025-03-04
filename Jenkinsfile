        pipeline{
            tools{
                jdk 'myjava'
                maven 'mymaven'
            }
            agent any
            stages{
                stage('Checkout'){
                    agent any
                    steps{
                echo 'cloning...'
                        git 'https://github.com/RayItern/DevOpsCodeDemo-1.git'
                    }
                }
                stage('Compile'){
                    agent {label 'slave1'}
                    steps{
                        echo 'compiling...'
                        sh 'mvn compile'
                }
                }
                stage('CodeReview'){
                    agent {label 'slave2'}
                    steps{
                    
                echo 'codeReview...'
                        sh 'mvn pmd:pmd'
                    }
                }
                stage('UnitTest'){
                    agent {label 'slave1'}
                    steps{
                    echo 'Testing'
                        sh 'mvn test'
                    }
                    post {
                    success {
                        junit 'target/surefire-reports/*.xml'
                    }
                }	
                }
                stage('Package on master') {
            agent {
                label 'master'
            }
            steps {
                echo 'Packaging...'
                sh 'mvn package'
            }
        }
    }
}


