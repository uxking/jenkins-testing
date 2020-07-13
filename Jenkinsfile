pipeline {
    agent {
        label 'jenkins-worker1'        
        }

    parameters {
     choice choices:['apple', 'bananas', 'peach'], description: 'Fruit Name. *** REQUIRED ***', name: 'Fruit_Name'
    }

    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    
    }

    stages {
        stage ('Python Requirements') {
            steps {
                echo "Installing the requirements for generating Hash" 
                sh 'python3 -m pip install -r requirements.txt'
            }
        }
        stage ('Validate Script & Generate Obfuscated Hash') {
            steps {
                echo "Gonna generate some data" 
                sh 'ehco 51*10 | bc'
                echo "Data done\n"
                echo "$Component_Name $Environment_Name $AWS_Region\n"
                sh "jtest.sh $Fruit_Name"
            }
        }
    }    
}
