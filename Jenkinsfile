pipeline {
  agent any     
        

  parameters {
     choice choices:['apple', 'bananas', 'peach'], description: 'Fruit Name. *** REQUIRED ***', name: 'Fruit_Name'
  }

  options {
      buildDiscarder(logRotator(numToKeepStr: '5'))
  
  }

  stages {
      stage ('Python Requirements') {
          steps {
              echo "Installing the python requirements"
              sh 'apt-get install pip3'
              sh 'python3 -m pip3 install -r requirements.txt'
          }
      }
      stage ('Produce a variable') {
          steps {
              echo "Gonna generate some data" 
              sh 'echo 51*10 | bc'
              echo "Data done\n"
              echo "$Component_Name $Environment_Name $AWS_Region\n"
              sh "jtest.sh $Fruit_Name"
          }
      }
  }   
}
