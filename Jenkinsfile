pipeline {
    agent {label 'master'}
    stages {
        stage('Build') {
	    steps {
	        bat 'python -m py_compile sources/add2vals.py sources/calc.py'
	    }
	}

	stage('Test') {
	    steps {
	        bat 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
	    }
	    post {
	        always {
		    junit 'test-reports/results.xml'
		}
	    }
	}

	stage('Deliver') {
	    steps {
	        bat 'pyinstaller --onefile sources/add2vals.py'
	    }
	    post {
	        success {
	            archiveArtifacts 'dist/add2vals*'
		}
	    }
	}
    }
}
