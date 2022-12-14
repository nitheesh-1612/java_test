pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        stage ('Build') {
            steps {
                echo 'Hello world'
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: '4d177004-3a5c-486c-8282-e339d95c902f', url: 'https://github.com/nitheesh-1612/java_project.git']]])
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }
      
        post {
            success {
                echo "build is success"
            }
            failure {
                echo "build is faileddddd"
            }
        }  
    }

        stage ('Deploy to tomcat server') {
            steps {
                deploy adapters: [tomcat9(credentialsId: '19f47c16-98f9-4f92-a0d6-004bb9ee6290', path: '', url: 'http://localhost:8070/')], contextPath: null, war: '**/*.war'
            }
        }
    
    }
}
