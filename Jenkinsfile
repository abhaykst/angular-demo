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
    withCredentials([<object of type com.cloudbees.jenkins.plugins.awscredentials.AmazonWebServicesCredentialsBinding>]) {      
      sh "aws s3 ls"
      sh "aws s3 cp ./dist/ --recursive s3://abhaybucket"
    }
  }
}
