pipeline {
    agent {
  label 'Workernode'
}

    stages {
  stage('Git clone') {
    steps {
      git 'https://github.com/sreepath363/samplejavaapp'
    }
post {
  success {
    echo 'Cloning completed'
  }
}
}
  stage('Code Compilation') {
    steps {
      sh '/opt/maven/bin/mvn compile'
    }
post {
  success {
    echo 'Code compliation completed'
    
  }
}
}
  stage('Code Review') {
    steps {
      sh '/opt/maven/bin/mvn -P metrics pmd:pmd'
    }
post {
  success {
    echo 'Code review completed'
    recordIssues(tools: [pmdParser(pattern: '**/pmd.xml')])
  }
}  
}
  stage('Unit Test') {
    steps {
      sh '/opt/maven/bin/mvn test'
    }
post {
  success {
    echo 'Unit test completed'
    junit 'target/surefire-reports/*.xml'
  }
}  
}
  stage('Code Coverage') {
    steps {
      sh '/opt/maven/bin/mvn verify'
    }
post {
  success {
    echo 'Code coverage is 50%'
    jacoco()
  }
}  
}
  stage('Package') {
    steps {
      sh '/opt/maven/bin/mvn package'
    }
post {
  success {
    echo 'War file generated'
  }
}   
}
}

}
