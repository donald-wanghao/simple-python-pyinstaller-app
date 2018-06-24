/*
 * Wang Hao adds the following jenkins pipeline configuration to test jenkins pipeline
 * functionality. I use python, pytest and pyinstaller tools to set up the three stages
 * of pipeline, i.e. "Build", "Test", "Deliver".
 *
 * In order to make pipeline run, you should install python, pip, pytest, pyinstaller on your
 * node first. I run it on a Windows 10 PC. If you want to run on a node other than Windows, please
 * change "bat" to "sh"
 * 2018-06-24
 *
 * Please use the Blue Ocean plugin to view the pipeline.  WH
 *
 */
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
	        bat 'pytest --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
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
