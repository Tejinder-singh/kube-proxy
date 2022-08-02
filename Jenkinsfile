pipeline {

    agent any
/*
	tools {
        maven "maven3"
    }
*/
    environment {
       
        registry = "http://44.197.180.149:8085"
        registryCredential = "nexus3"
	imagename = "my-docker-repo"    
       
    }



    stages{

        stage('BUILD'){
            steps {
                sh 'mvn clean install -DskipTests'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

      /*  stage('UNIT TEST'){
            steps {
                sh 'mvn test'
            }
        }

        stage('INTEGRATION TEST'){
            steps {
                sh 'mvn verify -DskipUnitTests'
            }
        }

        stage ('CODE ANALYSIS WITH CHECKSTYLE'){
            steps {
                sh 'mvn checkstyle:checkstyle'
            }
            post {
                success {
                    echo 'Generated Analysis Result'
                }
            }
        }

   
	    stage('CODE ANALYSIS with SONARQUBE') {

            environment {
                scannerHome = tool 'SonarQubeScanner'
            }

            steps {
                withSonarQubeEnv('sonarqube-8.9.9') {
                    sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=vprofile \
                   -Dsonar.projectName=vprofile-repo \
                   -Dsonar.projectVersion=1.0 \
                   -Dsonar.sources=src/ \
                   -Dsonar.java.binaries=target/test-classes/com/visualpathit/account/controllerTest/ \
                   -Dsonar.junit.reportsPath=target/surefire-reports/ \
                   -Dsonar.jacoco.reportsPath=target/jacoco.exec \
                   -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml'''
                }

                
            }
        }
	
	*/
	    
	    stage('Building image') {
            steps{
              script {
                dockerImage = docker.build imagename + ":$BUILD_NUMBER"
              }
            }
        }
        
        stage('Push Image') {
          steps{
            script {
              docker.withRegistry( registry,registryCredential ) {
                dockerImage.push("$BUILD_NUMBER")
                
              }
            }
          }
        }

   /*   stage('Kubernetes Deploy') {
	  agent { label 'KOPS' }
            steps {
                    sh "helm upgrade --install --force vproifle-stack helm/vprofilecharts --set appimage=${registry}:${BUILD_NUMBER} --namespace prod"
            }
        }   
	*/
       
    }


}
