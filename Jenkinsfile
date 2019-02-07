pipeline {
    agent any 
    triggers { 
        pollSCM('H/5 * * * *') 
    }
//    tools { 
//        maven 'Maven 3.6.0' 
//        jdk 'jdk8' 
//    }    
    stages {
        stage ('Initialize') {
            steps {
            	task('Properties') {
            		sh '''
	                    echo "PATH = ${PATH}"
	                    echo "M2_HOME = ${M2_HOME}"
                	'''    
            	}
            }
        }
        stage('Prepare') {
            steps {
            	task('checkout') {
            	    git url: 'https://github.com/id23cat/DMC-coreApi.git', 
            	    branch: 'master'
//            	    ,credentialsId: 'adp-tools-cat-risk-gdw-git-token-credentials-ph2'
            	}
				
				task('clean') {
					sh './mvn clean'    
				}
            }
        }
        stage('Build') { 
            steps {
                sh './mvn -Dmaven.test.failure.ignore=true install' 
            }
            post {
                success {
                    junit 'target/surefire-reports/**/*.xml' 
                }
            }
        }
        // stage('Test') { 
        //     steps {
        //         // 
        //     }
        // }
        // stage('Deploy') { 
        //     steps {
        //         // 
        //     }
        // }
    }
}