pipeline{
    agent none
    stages {  
        stage("Starting Dev") {
            agent any
            when {expression {"${env.BRANCH_NAME}"== "develop"}}
            steps{
                sleep 70
            }
        }
        stage("Starting Test") {
            agent any
            when {expression {"${env.BRANCH_NAME}"== "master"}}
            steps{
                sleep 55
            }
        }   
        stage('checkout SCM'){
            agent any
            when {expression {"${env.BRANCH_NAME}"== "develop"}}
            steps{
               git branch: 'master',url:'https://github.com/abhaykst/angular-demo.git'
            } 
        }
        stage('install node modules'){
            agent any
            when {expression {"${env.BRANCH_NAME}"== "develop"}}
            steps{
                sh "npm install"
            }
        }
        stage('build'){
            agent any
            when {expression {"${env.BRANCH_NAME}"== "develop"}}
            steps{
                sh "npm run build"
            }
        }
      
        stage('artifacts to s3 dev'){
            when {expression {return env.BRANCH_NAME == 'develop'}}
            agent any
            steps {
                withCredentials([[$class:'AmazonWebServicesCredentialsBinding',accessKeyVariable:'AWS_ACCESS_KEY_ID',credentialsId:'deploytos3',secretKeyVariable:'AWS_SECRET_ACCESS_KEY']]) {      
                    sh "aws s3 ls"      
                    sh "aws s3 sync ./dist/angular-demo/ s3://aaryabucket"
                }
            }
        }
        
    }   
}
