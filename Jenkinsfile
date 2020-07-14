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
      when { equals expected: 1, actual: currentBuild.number }
      steps {
        echo "Installing the python requirements"
        sh 'python3 -m pip install -r requirements.txt'
      }
    }
    stage ('Produce a variable') {
      steps {
        echo "The following parameter was passed in\n"
        echo "$Fruit_Name\n"
        echo "Setting an env variable called FINAL_FRUIT to be used in the next stage\n"
        script {
          env.FINAL_FRUIT = sh(script: "python3 ./jtest.py $Fruit_Name", returnStdout: true)
        }
      }
    }
    stage ('Use variable created above') {
      steps {
        echo "using the variable from above: ${env.FINAL_FRUIT} value\n"
        sh "ansible-playbook jtest.playbook.yml --extra-vars \"@jtest.vars.yml\" --extra-vars "\final_fruit=${env.FINAL_FRUIT}\""
      }
    }
  }
}
