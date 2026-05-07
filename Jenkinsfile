pipeline {
    agent any

    environment {
        K8S_NAMESPACE = 'webapps'
        CLUSTER_NAME  = 'EKS-1'
        SERVER_URL    = 'https://3B475DCEF944E228E6EC5B4DC72FABAB.gr7.us-east-1.eks.amazonaws.com'
    }

    stages {

        stage('Deploy To Kubernetes') {
            steps {
                withKubeCredentials(kubectlCredentials: [[
                    caCertificate: '',
                    clusterName:   "${CLUSTER_NAME}",
                    contextName:   '',
                    credentialsId: 'k8-token',
                    namespace:     "${K8S_NAMESPACE}",
                    serverUrl:     "${SERVER_URL}"
                ]]) {
                    sh "kubectl apply -f deployment-service.yml"
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                withKubeCredentials(kubectlCredentials: [[
                    caCertificate: '',
                    clusterName:   "${CLUSTER_NAME}",
                    contextName:   '',
                    credentialsId: 'k8-token',
                    namespace:     "${K8S_NAMESPACE}",
                    serverUrl:     "${SERVER_URL}"
                ]]) {
                    sh "kubectl get svc -n ${K8S_NAMESPACE}"
                    sh "kubectl get pods -n ${K8S_NAMESPACE}"
                }
            }
        }

    }
}
