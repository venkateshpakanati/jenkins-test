@Library('shared-jenkins-library') _

// pod label
def label = "pod-${UUID.randomUUID().toString()}-test"

//Jenkins workspace
def workingdir = "/home/jenkins"

images = [maven:"maven:3.5-jdk-8", mavenMemLmt:"2Gi", mavenCpuLmt:"1500m"]



//pipeline {
    // agent any
    //  stages {
      // stage('Test'){
        //    steps {
               // test()
            //    test {
                   
            //    }
            milestone ()
            try {
              timestamps {
                slaveTemplate = new test(label, images, workingdir, this)
                slaveTemplate.BuilderTemplate {
                   node(slaveTemplate.podlabel) {
                        stage ('Checkout Code') {
                            git branch: 'master',
                                credentialsId: '35205444-4645-4167-b50e-c65137059f09',
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
                                  sh "mvn clean compile"  
                                }
                                sh "ls -la ${pwd()}"
                                sh "ls -la ${pwd()}/first-stash"
                            }
                        }    
                    }
                }
              }
              
            } catch(e) {
                println $e
                throw e
            }   
         //   }
      //  }
  //  }
   
//}

//#!/usr/bin/groovy

// podTemplate(label: 'test-pod', 
//   containers: [
//     containerTemplate(
//       name: 'jnlp',
//       image: 'jenkinsci/jnlp-slave:3.10-1-alpine',
//       args: '${computer.jnlpmac} ${computer.name}'
//     ),
//     containerTemplate(
//       name: 'maven',
//       image: 'zenika/alpine-maven',
//       command: 'cat',
//       ttyEnabled: true
//     ),
//   ],
//   volumes: [ 
//     hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock'), 
//   ]
// )
// {
//  node('test-pod') {
//     stage ('Checkout Code') {
//         git branch: 'master',
//             credentialsId: '35205444-4645-4167-b50e-c65137059f09',
//             url: 'https://github.com/venkateshpakanati/microservices.git'

//         sh "ls -lat"
//         stash name: "first-stash", includes: "**/*"
//     }

//     stage ('Test stage') { 
//       container('maven') {
//         echo "under maven >>>>>>>>>>>>>>>>>>>>>>>"
//         sh 'mvn -version'
//         dir("first-stash") {
//           unstash "first-stash"
//           sh "mvn clean compile"  
//         }
//         sh "ls -la ${pwd()}"
//         sh "ls -la ${pwd()}/first-stash"
//       }
//     }
//   }
// }
