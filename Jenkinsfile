node {
 
stage ('limpiar') {
   
        sh 'mvn clean'
      }
 
  stage('Preparation') { // for display purposes
     // Get some code from a GitHub repository
     git 'https://github.com/johndavid93/soccer1.git'
  }
 stage ('Build') {
          
                sh 'mvn -Dmaven.test.failure.ignore=true install' 
            } 
 stage ('deploy UCD') {
   step([$class: 'UCDeployPublisher',
        siteName: 'local',
        component: [
            $class: 'com.urbancode.jenkins.plugins.ucdeploy.VersionHelper$VersionBlock',
            componentName: 'Jenkins John',
            createComponent: [
                $class: 'com.urbancode.jenkins.plugins.ucdeploy.ComponentHelper$CreateComponentBlock',
                componentTemplate: '',
                componentApplication: 'Jenkins'
            ],
            delivery: [
                $class: 'com.urbancode.jenkins.plugins.ucdeploy.DeliveryHelper$Push',
                pushVersion: '${BUILD_NUMBER}',
                baseDir: 'jobs\\test-ucd\\workspace\\build\\distributions',
                fileIncludePatterns: '*.war',
                fileExcludePatterns: '',
                pushProperties: 'jenkins.server=Local\njenkins.reviewed=false',
                pushDescription: 'Pushed from Jenkins',
                pushIncremental: false
            ]
        ]
    ])
 }
}
    

