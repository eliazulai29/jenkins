pipeline {
	agent any
    stages {
        stage('Build on k8 ') {
            steps {           
                        sh 'pwd'
                        sh 'cp -R helm/* .'
		        sh 'ls -ltr'
                        sh 'pwd'
                        sh '/usr/local/bin/helm upgrade --install eli-app petclinic  --set image.repository=eliazulai29/nginx-image:latest --set image.tag=1'
              			
            }           
        }
    }
}
