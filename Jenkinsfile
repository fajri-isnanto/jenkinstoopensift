node('skopeo') {

        def GIT_REPO = 'https://github.com/fajri-isnanto/jenkinstoopensift.git'
        def GIT_BRANCH = 'main'
        def DOCKER_IMAGE = 'my-docker-image:latest'
        def SONARQUBE_SCANNER = 'sonarqube-scanner' 
        def SONARQUBE_SERVER = 'http://sonar.sonarqube.svc.cluster.local:9000'   
        def OPENSHIFT_CLUSTER = 'https://api.openshift-cluster-url:6443' 
        def OPENSHIFT_PROJECT = 'my-project' 
        def SONARQUBE_TOKEN = 'sonar-fajri'
        def SONARQUBE_PROJECT = 'spring-helloWorld'      

    // def appName="petclinic"
    // def projectName="spring"
    // def repoUrl="github.com/carmensyva/spring-petclinic.git"
    // def branchName="main"

    // def intRegistryDev="default-route-openshift-image-registry.apps.dev.mibocp.co.id"
    // def ocpDRCDev="https://api.dev.mibocp.co.id:6443"
    // def hostedRepoUrl = "http://nexus-service.nexus.svc.cluster.local:8081/repository/mib-maven-hosted/"

        stage('Clone Repository') {
            
                git branch: "${GIT_BRANCH}", url: "${GIT_REPO}"
            
        }

        stage('SonarQube Analysis') {
                sh '''
                 mvn clean verify sonar:sonar \
                -Dsonar.projectKey="${SONARQUBE_PROJECT}" \
                -Dsonar.sources=src \
                -Dsonar.host.url="${SONARQUBE_SERVER}" \
                -Dsonar.login="${SONARQUBE_TOKEN}"
                '''    
        }

}