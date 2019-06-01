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
 node('test-pod') {
    stage ('Checkout Code') {
        git branch: 'master',
            credentialsId: 'f77386ce-bde4-4ddd-b127-f41a72168f79',
            url: 'https://github.com/venkateshpakanati/microservices.git'

        sh "ls -lat"
        stash name: "first-stash", includes: "**/*"
    }

    stage ('Test stage') { 
      container('maven') {
        echo "under maven >>>>>>>>>>>>>>>>>>>>>>>"
        sh 'mvn -version'
        dir("first-stash") {
          unstash "first-stash"
        }
        sh "ls -la ${pwd()}"
        sh "ls -la ${pwd()}/first-stash"
      }
    }
  }
}
