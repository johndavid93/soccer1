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
            componentName: 'Jenkins',
        ],

// implementar: inicia automáticamente un proceso de implementación en una importación exitosa.
        deploy: [
            $class: 'com.urbancode.jenkins.plugins.ucdeploy.DeployHelper$DeployBlock',

// deployApp, deployEnv y deployProc: la aplicación, el entorno y el proceso de aplicación que se ejecutarán.
            deployApp: 'Jenkins',
            deployEnv: 'Test',
            deployProc: 'Deploy Jenkins',

// deployReqProps: Especifique las propiedades del proceso de la aplicación.
            deployReqProps: 'AppProcessProp1=Value1\nAppProcessProp2=Value2',

// createProcess: Si el proceso de la aplicación no existe, esta especificación creará una.
            createProcess: [
                $class: 'com.urbancode.jenkins.plugins.ucdeploy.ProcessHelper$CreateProcessBlock',

// processComponent: especifique un proceso de un solo componente para inicializar el nuevo proceso de aplicación. Creará un solo paso Importar componente en un proceso de solicitud basado en el componente especificado anteriormente.
                processComponent: 'Deploy'
            ],

// deployVersions: Especifique qué versiones implementar. Sintaxis: COMPONENTE: VERSION. Separe el múltiplo con un nuevo carácter de línea (\ n).
            deployVersions: 'Jenkins:${BUILD_NUMBER}',

// deployOnlyChanged: especifique que solo se implemente en versiones modificadas.
            deployOnlyChanged: false,

// createSnapshot: crea una instantánea del entorno de implementación. 
// Si deployWithSnapshot es verdadero, la instantánea se creará primero y se usará para la implementación. 
// Además, si deployWithSnapshot es verdadero, las Versiones de implementación en el bloque de implementación se agregarán a la nueva instantánea, en lugar de usarse para la implementación.
            createSnapshot: [
               $class:'com.urbancode.jenkins.plugins.ucdeploy.DeployHelper$CreateSnapshotBlock',
                snapshotName: 'NameExample',
                deployWithSnapshot: false
            ]
        ]
    ])
}
}
    

