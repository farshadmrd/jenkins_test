pipeline {
    agent any

    tools {
        // Install the Maven version configured in Jenkins
        maven 'Maven 3.6.3'
        // Install the JDK version configured in Jenkins
        jdk 'JDK 17'
    }

   

 

    environment {
        // Define environment variables
        MAVEN_CLI_OPTS = '-B -DskipTests'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from version control
                git url: 'https://github.com/farshadmrd/jenkins_test.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                dir('microservices/hello-world') {
                    // Run Maven build
                    sh 'mvn clean package $MAVEN_CLI_OPTS'
                }
            }
        }

        stage('Test') {
            steps {
                dir('microservices/hello-world') {
                    // Run Maven tests
                    sh 'chmod +x ./mvnw'
                    sh './mvnw test'
                }
            }
        }

       
        stage('Package') {
            steps {
                dir('microservices/hello-world') {

                    // Run Maven package
                    sh 'mvn package'
                    echo 'Package created'
                    sh 'ls -l'
                    sh 'pwd'
                }

            }
        }
       

        stage('Checkout to test files') {
            steps {
                // Checkout code from version control
                git url: 'https://github.com/farshadmrd/testFiles_Jenkins.git', branch: 'main'
            }
        }
        
        stage('Setup Python') {
         
            steps {
                script{
                    
                    sh 'python --version'
                    sh 'ls -l'
                    sh 'pwd'
                    sh 'python simpleTest.py'


                }

            }
        }



        //deploy on mini kube
        // stage('Deploy') {
        //     steps {
        //         // Run Maven deploy
        //         sh 'mvn deploy'
        //     }
        // }
    }

    post {
        success {
            // Notify success
            echo 'Build and Test Successful'
        }
        failure {
            // Notify failure
            echo 'Build or Test Failed'
        }
    }
}
