node('PROD') {
    stage('Download GIT Repo') {
        try {
            git branch: 'main', url: 'https://github.com/santhoshpog/Listpython.git'
            sh 'date && sleep 30'
        }
        catch(exp) {
            echo "Error while cloning repo:${exp}"
        }
    }
}

stage('Run Dependencies') {
    stage('Serial Executor') {
        node('PROD') {
            try {
                sh 'python serial.py'
                sh 'date && sleep 20'
            }
            catch(exp) {
                echo "Error Executing Serial program:${exp}"
                sh "exit -1"//aborts pipeline
            }
        }
    }
    stage('Parallel Executor') {
        parallel linux: {
            node('PROD') {
                try {
                    git branch: 'main', url: 'https://github.com/santhoshpog/Listpython.git'
                    sh 'python evenodd.py'
                    sh 'date && sleep 20'
                }
                catch(exp) {
                    echo "Error with linux section:${exp}"
                    sh "exit -1" //to abort the pipeline for any failure
                }   
            }
        },
        windows: {
            node('PROD') {
                try {
                    git branch: 'main', url: 'https://github.com/santhoshpog/Listpython.git'
                    sh 'python dict.py'
                    sh 'date && sleep 20'
                }
                catch(exp) {
                    echo "Error in windows Section:${exp}"
                }
            }
        },
        Mac: {
            node('PROD') {
                try {
                    git branch: 'main', url: 'https://github.com/santhoshpog/Listpython.git'
                    sh 'python deploy.py'
                    sh 'date && sleep 20'
                }
                catch(exp) {
                    echo "Error in MAC section:${exp}"
                }
            }
        }
    stage('Final') {
        node('PROD') {
            try {
                git branch: 'main', url: 'https://github.com/santhoshpog/Listpython.git'
                echo 'This is the Final Stage' 
                sh 'date && sleep 10'
            }
            catch(exp) {
                echo "Error in Final Section:${exp}"
            }
        }
    }        
}
}
