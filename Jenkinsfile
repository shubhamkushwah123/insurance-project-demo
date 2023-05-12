node{
        stage('git checkout'){
            echo "checking out the code from github"
            git 'https://github.com/shubhamkushwah123/insurance-project-demo.git'
        }
        
        stage('maven build'){
            sh 'mvn clean package'
        }
        
        stage('build docker image'){
            sh 'docker build -t shubhamkushwah123/insure-me:1.0 .'
        }
        
        stage('push docker image to docker hub registry')
        {
            echo 'pushing images to registry'
            
            withCredentials([string(credentialsId: 'docker-hub-password', variable: 'dockerHubPassword')]) {
                sh "docker login -u shubhamkushwah123 -p ${dockerHubPassword}"
                sh 'docker push shubhamkushwah123/insure-me:1.0'
            }
        }
        
        stage('configure test-server and deploy insure-me'){
            echo "configuring test-server"
          //  sh 'ansible-playbook configure-test-server.yml'
            ansiblePlaybook become: true, credentialsId: 'ssh-key-ansibles', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: 'configure-test-server.yml'
        }
        
}
