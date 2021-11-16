node ('master') {

    stage ('scm_checkout'){
        checkout([$class: 'GitSCM', 
        branches: [[name: '*/master']], 
        extensions: [], 
        userRemoteConfigs: [[url: 'https://github.com/abheethy/Maven-petclinic-project.git']]])
    }
    
    
    stage ('build'){
        sh 'mvn clean install'
    }

    input 'Proceed with Deployment?'

    stage ('artifactory') {
       sh 'curl -uuser1:AP3wgCK5cmUdGA9uDryy7drWJrB -T target/petclinic.war "https://plussforum.jfrog.io/artifactory/petclinic-generic-local/petclinic.war"'
    }

    stage ('archive') {
        archiveArtifacts artifacts: 'target/*.war', followSymlinks: false
    }  
}
