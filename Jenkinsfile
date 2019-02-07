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
            	sh '''
            		echo "PATH = ${PATH}"
            		echo "M2_HOME = ${M2_HOME}"
            	'''    
            	}
            }       
        stage('Prepare') {
            steps {
            	git url: 'https://github.com/id23cat/DMC-coreApi.git', 
            		branch: 'master'
//            	    ,credentialsId: 'adp-tools-cat-risk-gdw-git-token-credentials-ph2'
            	sh './mvnw clean'
            }
        }
        stage('Build') { 
            steps {
                sh './mvnw -Dmaven.test.failure.ignore=true install' 
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