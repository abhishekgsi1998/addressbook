pipeline {

      agent any

      stages {

            stage('GIT') {

                  steps {

                        echo 'Hi, this is Abhishek from 3Pillar'

                        echo 'We are Starting the Testing'
                        git 'https://github.com/abhishekgsi1998/addressbook.git'

                  }

            }
            stage('COMPILE_packege') {

                  steps {

       
                        echo 'COMPILE THE FILE'
                        tool name: 'local_mvn', type: 'maven'
                        sh 'mvn -f pom.xml package'
                        


                  }

            }

            stage('Build') {

                  steps { 

                        echo 'Building Sample Maven Project'
                        archiveArtifacts '**/*.war'

                  }

            }
            stage('Test') {

                  steps {

                        echo 'Testing'
                       junit '**/target/surefire-reports/*.xml'

                  }

            }
          
            stage('Deploy') {

                  steps {

                        echo 'Deploying Sample Maven Project'
                        copyArtifacts filter: '**/*.war', fingerprintArtifacts: true, projectName: 'Pipe', selector: lastWithArtifacts()
                        deploy adapters: [tomcat8(credentialsId: '14d61449-17df-4401-8ab0-2fca8f2424a4', path: '', url: 'http://3.84.15.237:9090/')], contextPath: '/', war: '**/*.war'
                  }

            }
             

      }

}
