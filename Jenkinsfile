pipeline {
   agent any

   stages {
      stage('checkout_Code_integration') {
         steps {
            checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'd4450660-71ed-4a73-8c48-30b80808023f', url: 'https://github.com/AvinashArnav/CICD.git']]])

         }
      }
      stage('Unit_Testing') {
         steps {
                        sh "/usr/local/bin/pip install -r requirements.txt"
            sh "/usr/bin/python -m pytest -v tests/test_generator.py"
         }
      }
      stage('Docker_image_Build') {
         steps {

            sh "/usr/bin/docker build -t aviarnav/cicd-example:latest ."

         }
      }
      stage('publish') {
         steps {
			withDockerRegistry(credentialsId: 'dockerhub') {
    // some block
}
         }
      }
      stage('Running_image_from_DockerHub') {
         steps {

           sh "/usr/bin/docker run -p 5000:5000 --rm aviarnav/cicd-example:latest"
         }
         }
      }
   }
