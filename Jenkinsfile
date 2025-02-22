pipeline {
    agent any

    environment{
        registry = 'xuannguyenhehe/house-price-prediction-api'
        registryCredential = 'dockerhub'
    }

    stages {
        stage('Deploy') {
            agent {
                kubernetes {
                    containerTemplate {
                        name 'helm' // Name of the container to be used for helm upgrade
                        image 'cristiano2003/custom-jenkins:0.0.3' // The image containing helm
                        alwaysPullImage true // Always pull image in case of using the same tag
                    }
                }
            }
            steps {
                script {
                    container('helm') {
                        // Install Helm before using it
                        sh '''
                            curl https://baltocdn.com/helm/signing.asc | tee /etc/apt/trusted.gpg.d/helm.asc
                            curl https://baltocdn.com/helm/stable/deb/helm-stable-deb.repo | tee /etc/apt/sources.list.d/helm-stable-deb.list
                            apt-get update && apt-get install -y helm
                        '''
                        // Use Helm to deploy
                        sh("helm upgrade --install hpp ./helm-charts/hpp --namespace model-serving")
                    }
                }
            }
        }
    }
}
