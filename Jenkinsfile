pipeline {
    agent any
    stages {
        //Continuous Integration
        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests=true'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        //Continuous Delivery
          stage('Upload-to-Nexus') {
            steps {
                nexusArtifactUploader artifacts: [
                    [
                        artifactId: 'numeric',
                        classifier: '',
                        file: 'target/numeric-0.0.1.jar',
                        type: 'jar'
                    ]
                ],
                credentialsId: 'nexus',
                groupId: 'com.devops',
                nexusUrl: '34.228.143.204:8081',
                nexusVersion: 'nexus3',
                protocol: 'http',
                repository: 'compare-service',
                version: '0.0.1-$BUILD_NUMBER'
            }
        }
        //stage('Docker Build&Push') {
        //    steps {
        //        withDockerRegistry(credentialsId: 'Docker', url: "") {
        //            sh 'docker build -t issaouidevops/compare-app .'
        //            sh 'docker push issaouidevops/compare-app'
        //        }
        //    }
        //}
        //Continuous Deployment
        //stage('Deploy') {
        //    steps {
        //        withDockerRegistry(credentialsId: 'Docker', url: "") {
        //            sh 'docker -H ssh://ubuntu@172.31.42.35 run -d --name myapp -p 8082:8080 issaouidevops/compare-app'
        //        }
        //    }  
        //}

    }
}
