// @Library('shared-jenkins-library') _
// pipeline {
//     agent any
    
//     stages {
//        stage('Test'){
//             steps {
//                // test()
//                test {
                   
//                }
//             }
//         }
//     }
   
// }

//#!/usr/bin/groovy

podTemplate(label: 'test-pod', 
  containers: [
    containerTemplate(
      name: 'jnlp',
      image: 'jenkinsci/jnlp-slave:3.10-1-alpine',
      args: '${computer.jnlpmac} ${computer.name}'
    ),
    containerTemplate(
      name: 'maven',
      image: 'zenika/alpine-maven',
      command: 'cat',
      ttyEnabled: true
    ),
  ],
  volumes: [ 
    hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock'), 
  ]
)
{
  node  {
    stage ('Checkout Code') {
        git branch: 'master',
            credentialsId: '35205444-4645-4167-b50e-c65137059f09',
            url: 'ssh://github.com/venkateshpakanati/microservices.git'

        sh "ls -lat"
    }

    stage ('Test stage') { 
      container('maven') {
       echo "under maven >>>>>>>>>>>>>>>>>>>>>>>"
      }
    }
  }
}