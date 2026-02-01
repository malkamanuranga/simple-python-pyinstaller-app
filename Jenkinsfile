pipeline {
    agent any
    options {
        // This stops the pipeline if the tests are "unstable" (some fail)
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') {
            steps {
                sh 'python -m py_compile sources/add2vals.py sources/calc.py'
                stash(name: 'compiled-results', includes: 'sources/*.py*')
            }
        }
        stage('Test') {
            steps {
                sh 'py.test --junit-xml test-reports/results.xml sources/test_calc.py'
            }
            post {
                always {
                    junit 'test-reports/results.xml'
                }
            }
        }
        stage('Deliver') { 
            steps {
                // Bundles the app into a single standalone executable
                sh "pyinstaller --onefile sources/add2vals.py" 
            }
            post {
                success {
                    // Saves the executable so you can download it from the UI
                    archiveArtifacts 'dist/add2vals' 
                }
            }
        }
    }
}