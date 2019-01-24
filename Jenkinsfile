node {
  agent any
   tools {
        maven 'Maven 3.5.4'
        jdk 'jdk8'
    }
 
  stage('Preparation') { // for display purposes
     // Get some code from a GitHub repository
     git 'https://github.com/johndavid93/soccer1.git'
  }
 stage ('Build') {
            steps {
                sh 'mvn -Dmaven.test.failure.ignore=true install' 
            }
}
