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

podTemplate(label: 'twistlock-example-builder', 
  containers: [
    containerTemplate(
      name: 'jnlp',
      image: 'jenkinsci/jnlp-slave:3.10-1-alpine',
      args: '${computer.jnlpmac} ${computer.name}'
    ),
    containerTemplate(
      name: 'alpine',
      image: 'twistian/alpine:latest',
      command: 'cat',
      ttyEnabled: true
    ),
  ],
  volumes: [ 
    hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock'), 
  ]
)
{
  node ('twistlock-example-builder') {

    stage ('Pull image') { 
      container('alpine') {
        sh """
        curl --unix-socket /var/run/docker.sock \ 
             -X POST "http:/v1.24/images/create?fromImage=nginx:stable-alpine"
        """
      }
    }


  }
}