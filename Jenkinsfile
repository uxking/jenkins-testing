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
              
              sh 'python3 -m pip install -r requirements.txt'
          }
      }
      stage ('Produce a variable') {
          steps {
              echo "Gonna generate some data" 
              sh "echo 51*10 | bc"
              echo "Data done\n"
              echo "$Fruit_Name\n"
              sh "./jtest.sh $Fruit_Name"
          }
      }
  }   
}
