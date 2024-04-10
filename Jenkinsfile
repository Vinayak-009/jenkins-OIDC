pipeline {
    agent any
    stages {
       stage("Generating OIDC token and saving it to a file") {
            steps {
                script {
                        sh (script: 'gcloud auth print-identity-token default-one@use-case-416807.iam.gserviceaccount.com  --audiences="//iam.googleapis.com/projects/493585028974/locations/global/workloadIdentityPools/jenkins"  > /usr/share/token/credential.key',returnStdout: true)
                }
            }
        }
        stage ("getting the WIF config file into a variable")
        {
            steps {
                     withCredentials([file(credentialsId: 'wif-config-file', variable: 'WIF')]) 
                        {
                         sh '''
                            gcloud auth login --brief --cred-file=$WIF --quiet
                            gcloud container clusters list
                            gcloud compute instances list
                            '''

                        }
                }
        }
    }    
}
