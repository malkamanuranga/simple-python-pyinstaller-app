pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                // This compiles the python files to check for syntax errors
                sh 'python -m py_compile sources/add2vals.py sources/calc.py' 
                
                // This "saves" the files so the next stage can use them
                stash(name: 'compiled-results', includes: 'sources/*.py*') 
            }
        }
    }
}