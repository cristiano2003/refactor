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
                        image 'xuannguyenhehe/custom-jenkins:0.0.3' // The image containing helm
                        alwaysPullImage true // Always pull image in case of using the same tag
                    }
                }
            }
            steps {
                script {
                    container('helm') {
                        sh("helm upgrade --install hpp ./helm-charts/hpp --namespace model-serving")
                    }
                }
            }
        }
    }
}
