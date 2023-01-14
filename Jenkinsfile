def flag = false

pipeline {
    agent none
    stages {
        stage('1 - Always') {
            agent{ label 'built-in'}
            steps {
                git branch: 'main', url: 'https://github.com/Michael-Shen/Python'
                echo 'stage1'
                echo pwd()
                bat 'dir'
            }
        }

        stage('2 - Maybe') {
           agent {label 'agent1'}

            steps {
                echo 'stage2'
                script { 
                    if (true){   //under some conditions , change the flag
                        flag = true 
                        echo 'in agent1'
                        sh 'ls -al'
                    }
                        
                    }
            }
        }

        stage('3 - If Maybe was executed') {
            agent any
            when { expression { flag == true } }

            steps {
                echo "stage3"
                echo "/$flag is $flag"
            }
        }
    }
}
