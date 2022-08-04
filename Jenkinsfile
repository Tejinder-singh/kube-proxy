pipeline {

    agent any
/*
	tools {
        maven "maven3"
    }
*/
    environment {
       
        registry1 = "http://44.197.180.149:8085"
        registryCredential = "nexus3"
	imagename = "my-docker-repo"    
	registry = "442376613065.dkr.ecr.us-east-1.amazonaws.com/my-kube"
       
    }



    stages{
   /*	    

       stage('UNIT TEST'){
            steps {
                sh 'mvn test1'
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
	
	
	    
	    stage('Building image') {
            steps{
              script {
                dockerImage = docker.build registry
              }
            }
        }
        
        stage('Push Image') {
          steps{
            script {
		    sh "aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 442376613065.dkr.ecr.us-east-1.amazonaws.com"
		    sh "docker push 442376613065.dkr.ecr.us-east-1.amazonaws.com/my-kube"
                    
            }
          }
        }
*/
	    stage('K8s Deploy') {
                steps {
		     withKubeConfig(caCertificate: '', clusterName: '', contextName: '', credentialsId: 'k8s', namespace: '', serverUrl: '') {
		      sh "/home/ec2-user/bin/kubectl apply -f eks-deploy-k8s.yaml"  			                           
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

