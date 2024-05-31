node{
    stage('git checkout'){
        git 'https://github.com/VivianFernandes777/Staragilefinance'
    }
   
    stage('build and package'){
        sh 'mvn clean package'
    }
      stage('selenium test'){
        sh 'mvn test'
    }
    
    
    stage('build and package'){
        sh 'docker build -t vivianfernandes777/staragilefinance:v1 .'
        sh 'docker images'
    }
    
     stage('Docker login & push ') {
      withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
        sh "echo $PASS | docker login -u $USER --password-stdin"
        sh 'docker push vivianfernandes777/staragilefinance:v1'
         }
     }     
     
     stage('Deploy on ansible') {
      ansiblePlaybook become: true, credentialsId: 'ansible', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: 'ansible-playbook.yml', vaultTmpPath: ''
        }
            
}
