pipeline {
    agent any  // This specifies that the pipeline can run on any available agent
    
    environment {
        PATH = "/opt/maven/bin:$PATH"
    }
    
    stages {
        stage('checkout') {
            steps {
                git branch: 'main', credentialsId: 'git_credentials', url: 'https://github.com/Chinmayi2019/HelloServlet.git'
                echo 'checkout successful'
            }
        }
        
        stage('build') {
            steps {
                sh "mvn clean package"
                echo 'build successful'
            }
        }
        
        stage('Deploy') {
            steps {
                sshagent(['deploy_user']) {
                    sh "scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/PJob-1/target/helloworld.war ec2-user@3.86.208.15:/opt/apache-tomcat-9.0.93/webapps"
                }
                echo 'deploy successful'
            }
        }
    }
}
