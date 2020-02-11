pipeline {

      agent any

      stages {

            stage('GIT') {

                  steps {

                        echo 'Hi, this is Hemant from 3Pillar'

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
                        copyArtifacts filter: '**/*.war', fingerprintArtifacts: true, projectName: 'addressbook', selector: lastWithArtifacts()
                        deploy adapters: [tomcat8(credentialsId: '14d61449-17df-4401-8ab0-2fca8f2424a4', path: '', url: 'http://54.208.118.156:9090/')], contextPath: '/', war: '**/*.war'
                  }

            }
             

      }

}
