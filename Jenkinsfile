node {
  stage('checkout SCM'){
    git branch: 'master',url:'https://github.com/abhaykst/angular-demo.git'  
  }
  stage('install node modules'){
    sh "npm install"
  }
  stage('build'){
    sh "npm run build"
  }
  stage('artifacts to s3'){
    withCredentials([[$class:'AmazonWebServicesCredentialsBinding',accessKeyVariable:'AWS_ACCESS_KEY_ID',credentialsId:'deploytos3',secretKeyVariable:'AWS_SECRET_ACCESS_KEY']]) {      
      sh "aws s3 ls"      
      sh "aws s3 sync ./dist/ s3://abhaybucket"
    }
  }
}
