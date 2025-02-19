pipeline{
    agent any
    tools{
        jdk 'jdk17'
        nodejs 'node23'
    }
    environment{
        SCANNER_HOME=tool 'sonar-scanner'
    }
    stages{
        stage('Clean Workspace'){
            steps{
                cleanWs()
            }
        }
        stage('Git Checkout'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'git@github.com:sdeep1096/starbucks.git']])
            }
        }
        stage('SonarQube Analysis'){
            steps{
                withSonarQubeEnv('sonar-server'){
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=starbucks \
                        -Dsonar.projectKey=starbucks '''
                }
            }
        }
        stage('quality gate'){
            steps{
                script{
                    waitForQualityGate abortPipeline: false,credentialsId: 'sonar-token'
                }
            }
        }
        stage('Install Dependencies'){
            steps{
                sh 'npm install'
            }
        }
        stage('OWASP File System Scan'){
            steps{
                dependencyCheck additionalArguments: '--scan ./ --disableYarnAudit --disableNodeAudit', odcInstallation: 'DP-Check'
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }
        stage('Trivy File Scan'){
            steps{
                sh 'trivy fs . > trivyfs.txt'
            }
        }
        stage('Docker Build and Push'){
            steps{
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker'){
                        sh 'docker build -t briarheart1096/starbucks:latest .'
                        sh 'docker push briarheart1096/starbucks:latest'
                    }
                }
            }
        }
        stage('Trivy'){
            steps{
                sh 'trivy image briarheart1096/starbucks:latest > trivy.txt'
            }
        }
        stage('Deploy to Container'){
            steps{
                sh 'docker run -d --name swiggy -p 30000:30000 briarheart1096/starbucks:latest'
            }
        }
    }
}
