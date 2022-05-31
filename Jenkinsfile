pipeline {
    agent any
    environment {
        PROJECT_ID = 'project-id'
        CLUSTER_NAME = 'cluster-name'
        CLUSTER_LOCATION = 'northamerica-northeast2'
        CREDENTIALS_ID = 'credentials-id'
        SCANNER_HOME = tool 'SonarQubeScanner'
        ORGANIZATION = "revature-reverse-project"
        PROJECT_NAME = "User-Service"
    }
    stages {
        stage('Quality Gate') {
            steps {
                echo "Quality Gate"
                withSonarQubeEnv('SonarCloud') {
                    sh 'mvn clean install sonar:sonar'
                    sh '''$SCANNER_HOME/bin/sonar-scanner -Dsonar.organization=$ORGANIZATION \
                    -Dsonar.java.binaries=target/classes/ \
                    -Dsonar.projectKey=$PROJECT_NAME \
                    -Dsonar.sources=.'''
                }
            }
        }
        /*
        stage('Unit Tests') {
            steps {
                echo "Unit Tests"
                sh "mvn test"
            }
        }
        stage ('Docker Build') {
            steps {
                script {
                    echo "Docker Build"
                    sh "docker build -t user-service ."
                }
            }
        }
        stage ('Docker tag and push to Github') {
            steps {
                script {
                    echo "Docker push"
                    sh "docker tag user-service ghcr.io/${GITHUB_USER}/user-service"
                    sh "docker push ghcr.io/${GITHUB_USER}/user-service"
                }
            }
        }
        stage ('Deploy to GKE') {
            steps {
                echo "Deploying to GKE"
                step([$class: 'KubernetesEngineBuilder',
                    projectId: env.PROJECT_ID,
                    clusterName: env.CLUSTER_NAME,
                    location: env.CLUSTER_LOCATION,
                    manifestPattern: 'deployment',
                    credentialsId: env.CREDENTIALS_ID,
                    verifyDeployments: true])
            }
        }
        */
    }
}