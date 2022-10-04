pipeline{
agent {label 'my-new-slave'}
triggers {
        pollSCM '* * * * *'
    }
    stages{
        stage('checkout'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'e7690690-7cec-4ae4-9ed0-54988d19b17c', url: 'https://github.com/Shrveenpk/mavenrepo.git']]])
            }
        }
        
        stage('build'){
            steps{
                sh 'mvn package'
            }
        }
        
                stage('sonar'){
            steps{
                withSonarQubeEnv('sonar-new') {
    sh 'mvn sonar:sonar'
    
                }
}
        }
        
                stage('nexus'){
            steps{
                sh 'mvn deploy'
            }
        }
        
                stage('tomcat'){
            steps{
                sh 'scp /root/workspace/sample/target/studentapp-2.5-SNAPSHOT.war 35.183.40.95:/var/lib/tomcat/webapps'
            }
        }
        
        
        
    }
}
