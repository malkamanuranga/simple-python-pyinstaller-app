pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                sh 'python -m py_compile sources/add2vals.py sources/calc.py' 
                stash(name: 'compiled-results', includes: 'sources/*.py*') 
            }
        }
        stage('Test') { 
            steps {
                // Runs the tests and saves results to an XML file
                sh 'pytest --verbose --junit-xml test-reports/results.xml sources/test_calc.py' 
            }
            post {
                always {
                    // This tells Jenkins to display the test results in the UI
                    junit 'test-reports/results.xml' 
                }
            }
        }
    }
}