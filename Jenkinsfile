pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/fajri-isnanto/jenkinstoopensift.git'
        GIT_BRANCH = 'main'
        DOCKER_IMAGE = 'my-docker-image:latest'
        SONARQUBE_SCANNER = 'sonarqube-scanner' 
        SONARQUBE_SERVER = 'http://sonar.sonarqube.svc.cluster.local:9000'   
        OPENSHIFT_CLUSTER = 'https://api.openshift-cluster-url:6443' 
        OPENSHIFT_PROJECT = 'my-project' 
        SONARQUBE_TOKEN = 'sonar-fajri'
        SONARQUBE_PROJECT = 'spring-helloWorld'      
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: "${GIT_BRANCH}", url: "${GIT_REPO}"
            }
        }

        stage('SonarQube Analysis') {
            steps {
                sh '''
                sonar-scanner \
                -Dsonar.projectKey="${SONARQUBE_PROJECT}" \
                -Dsonar.sources=src \
                -Dsonar.host.url="${SONARQUBE_SERVER}" \
                -Dsonar.login="${SONARQUBE_TOKEN}"
                '''
            }
        }

        // stage('Build in OpenShift') {
        //     steps {
        //         script {
        //             openshift.withCluster("${OPENSHIFT_CLUSTER}") {
        //                 openshift.withProject("${OPENSHIFT_PROJECT}") {
        //                     sh "oc start-build ${DOCKER_IMAGE} --follow"
        //                 }
        //             }
        //         }
        //     }
        // }

        // stage('Trivy Image Scan') {
        //     steps {
        //         script {
        //             sh "trivy image --severity HIGH,CRITICAL ${DOCKER_IMAGE}"
        //         }
        //     }
        // }

        // stage('Deploy to OpenShift') {
        //     steps {
        //         script {
        //             openshift.withCluster("${OPENSHIFT_CLUSTER}") {
        //                 openshift.withProject("${OPENSHIFT_PROJECT}") {
        //                     sh "oc rollout latest dc/${DOCKER_IMAGE}"
        //                 }
        //             }
        //         }
        //     }
        // }
    }

    // post {
    //     always {
    //         cleanWs() // Clean workspace after build
    //     }
    // }
}