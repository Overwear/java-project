pipeline {
    agent {label '31bfaa9835ad'}
    stages {
        stage('Unit Testing') {
            steps {
                echo 'Testing..'
                //sh 'ant -f test.xml -v'
            }
        }
        stage('Build') {
            steps {
                echo 'Building..'
                //sh 'ant -f build.xml -v
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                sh 'aws s3 cp dist/rectangle-${BUILD_NUMBER}.jar s3://hw-10-yee/'
            }
        }
        stage('Report') {
            steps {
                echo 'Generating Report...'
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'AWS', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) 
                {    
                    sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins'
                }
    }
}