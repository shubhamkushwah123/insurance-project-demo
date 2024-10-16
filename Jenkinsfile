node{
    
    stage('checkout'){
        git 'https://github.com/shubhamkushwah123/insurance-project-demo.git'
    }
    
    stage('maven build'){
        sh 'mvn clean package'
    }
    
    stage('containerize'){
      //  sh 'docker build -t shubhamkushwah123/insure-me:1.0 .'
    }
    
    stage('Release'){
        withCredentials([string(credentialsId: 'dockerHubPwd', variable: 'dockerHubPwd')]) {
      //  sh "docker login -u shubhamkushwah123 -p ${dockerHubPwd}"
     //   sh 'docker push shubhamkushwah123/insure-me:1.0'
        }
    }
    
    stage('Deploy to Test'){
     ansiblePlaybook become: true, credentialsId: 'ansible-key', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: 'configure-test-server.yml', vaultTmpPath: ''
    }
    
    stage('checkout regression test source code'){
        git 'https://github.com/shubhamkushwah123/my-selenium-test-app.git'
    }
    
    stage('build test scripts'){
        sh 'mvn clean package assembly:single'
    }
    
    stage('execute selenium test script'){
        sh 'java -jar target/my-app-test-0.0.1-SNAPSHOT-jar-with-dependencies.jar'
    }

    stage('checkout'){
        git 'https://github.com/shubhamkushwah123/insurance-project-demo.git'
    }
    
     stage('Deploy to Test'){
     ansiblePlaybook become: true, credentialsId: 'ansible-key', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: 'configure-prod-server.yml', vaultTmpPath: ''
    }
    
    
    
}
