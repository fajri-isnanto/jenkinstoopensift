pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/fajri-isnanto/jenkinstoopensift.git'
        GIT_BRANCH = 'main'
        DOCKER_IMAGE = 'my-docker-image:latest'
        SONARQUBE_SCANNER = 'sonarqube-scanner' // Name of the SonarQube Scanner tool configured in Jenkins
        SONARQUBE_SERVER = 'sonarqube-server'   // Name of the SonarQube server configured in Jenkins
        OPENSHIFT_CLUSTER = 'https://api.openshift-cluster-url:6443' // OpenShift cluster URL
        OPENSHIFT_PROJECT = 'my-project'       // OpenShift project name
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: "${GIT_BRANCH}", url: "${GIT_REPO}"
            }
        }

        stage('Scanning By SonarQube ') {
            steps {
                script {
                    def scannerHome = tool "${SONARQUBE_SCANNER}"
                    withSonarQubeEnv("${SONARQUBE_SERVER}") {
                        sh  "${scannerHome}/bin/sonar-scanner -X"
                    }
                }
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

    post {
        always {
            cleanWs() // Clean workspace after build
        }
    }
}