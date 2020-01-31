pipeline {

      agent any

      stages {

            stage('GIT') {

                  steps {

                        echo 'Hi, this is Hemant from 3Pillar'

                        echo 'We are Starting the Testing'
                        git 'https://github.com/HemantTomar/addressbook.git'

                  }

            }
            stage('COMPILE_packege') {

                  steps {

       
                        echo 'COMPILE THE FILE'
                        tool name: 'Local_maven', type: 'maven'
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
                        deploy adapters: [tomcat9(credentialsId: '401dcb97-d3c5-4ffd-9f9e-8be2c777980e', path: '', url: 'http://3.19.67.153:9090/')], contextPath: '/', war: '**/*.war'
                  }

            }
              stage('mail') {
        steps {
            
               emailext (to: 'hemant14750@gmail.com', replyTo: 'hemant14750@gmail.com', subject: "Email Report from - '${env.JOB_NAME}' ", body: readFile("/var/lib/jenkins/workspace/addressbook/addressbook_main/target/surefire-reports/com.edurekademo.utilities.TestLogger.txt"), mimeType: 'html/txt');
        }
    }


      }

}
