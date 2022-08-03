pipeline{
    agent none
    stages {  
        stage("Starting Dev") {
            agent any
            when {expression {"${env.BRANCH_NAME}"== "develop"}}
            steps{
                sleep 10
            }
        }
        stage("Starting production") {
            agent any
            when {expression {"${env.BRANCH_NAME}"== "master"}}
            steps{
                sleep 20
            }
        }   
        stage('checkout SCM develop branch'){
            agent any
            when {expression {"${env.BRANCH_NAME}"== "develop"}}
            steps{
               git branch: 'develop',url:'https://github.com/abhaykst/angular-demo.git'
            } 
        }
      
       stage('checkout SCM master branch'){
            agent any
            when {expression {"${env.BRANCH_NAME}"== "master"}}
            steps{
               git branch: 'master',url:'https://github.com/abhaykst/angular-demo.git'
            } 
        }
        stage('install node modules development'){
            agent any
            when {expression {"${env.BRANCH_NAME}"== "develop"}}
            steps{
                sh "npm install"
            }
        }
      
      stage('install node modules for development'){
            agent any
            when {expression {"${env.BRANCH_NAME}"== "master"}}
            steps{
                sh "npm install"
            }
        }
        stage('build... devepment envionment'){
            agent any
            when {expression {"${env.BRANCH_NAME}"== "develop"}}
            steps{
                sh "npm run build"
            }
        }
      
      stage('build... production envionment'){
            agent any
            when {expression {"${env.BRANCH_NAME}"== "master"}}
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
        stage('artifacts to s3 production'){
            when {expression {return env.BRANCH_NAME == 'master'}}
            agent any
            steps {
                withCredentials([[$class:'AmazonWebServicesCredentialsBinding',accessKeyVariable:'AWS_ACCESS_KEY_ID',credentialsId:'deploytos3',secretKeyVariable:'AWS_SECRET_ACCESS_KEY']]) {      
                    sh "aws s3 ls"      
                    sh "aws s3 sync ./dist/angular-demo/ s3://abhaybucket"
                }
            }
        }
        
    }   
}
