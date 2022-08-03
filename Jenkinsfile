node {
  stage('checkout SCM'){
    git branch: 'master',url:'https://github.com/abhaykst/angular-demo.git'  
  }
  stage('install node modules'){
    sh "npm install"
  }
}
