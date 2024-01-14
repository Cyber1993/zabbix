#!groovy
//  groovy Jenkinsfile
properties([disableConcurrentBuilds()])\

pipeline  {
        agent { 
           label ''
        }

    options {
        buildDiscarder(logRotator(numToKeepStr: '10', artifactNumToKeepStr: '10'))
        timestamps()
    }
    stages {
        stage("Git clone") {
            steps {
                sh '''
                cd /var/lib/jenkins/workspace/
                rm -rf ansible-jenkins
                git clone https://github.com/Cyber1993/ansible-jenkins.git
                '''
            }                
        }    
        stage("Build") {
            steps {
                sh '''
                cd /var/lib/jenkins/workspace/ansible-jenkins/Ansinle
                docker build -t yurashupik/md221 .
                '''
            }
        } 
        stage("docker run") {
            steps {
                sh '''
                docker run \
                --name ansible \
                -d yurashupik/md221
                '''
            }
        }
        stage("docker login") {
            steps {
                echo " ============== docker login =================="
                withCredentials([usernamePassword(credentialsId: 'yurashupikjenkins', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    script {
                        def loginResult = sh(script: "docker login -u $USERNAME -p $PASSWORD", returnStatus: true)
                        if (loginResult != 0) {
                            error "Failed to log in to Docker Hub. Exit code: ${loginResult}"
                        }
                    }
                }
                echo " ============== docker login completed =================="
            }
        }

        stage("docker push") {
            steps {
                echo " ============== pushing image =================="
                sh '''
                docker push yurashupik/md221
                '''
            }
        }
    }
}
