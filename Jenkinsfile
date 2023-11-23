node{

    stage('code checkout'){
        git 'https://github.com/shubhamkushwah123/capstone-project-demo.git'
    }
    
    stage('build'){
      sh 'mvn clean package'  
    }
    
    stage('package as docker image'){
      sh 'docker build -t shubhamkushwah123/insure-me:1.0 .'
    }
    
    stage('push to dockerhub'){
      withCredentials([string(credentialsId: 'docker-hub-password', variable: 'dockerHubPassword')]) {
            sh "docker login -u shubhamkushwah123 -p ${dockerHubPassword}"
            sh 'docker push shubhamkushwah123/insure-me:1.0'
        }
    }
    
    stage('deploy to test-environment') {
        ansiblePlaybook become: true, credentialsId: 'ansible-ssh-jenkins-key', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: 'configure-test-server.yml'
    }
    
    
    
}
