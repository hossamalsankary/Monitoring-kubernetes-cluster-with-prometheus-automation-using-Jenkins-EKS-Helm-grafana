pipeline{
    agent any
    stages{

        stage("Install Deplancey"){
            steps{
              

                sh 'chmod +x -R ./bashScripts/CheckIfEksctlIsExist.sh  '
                 sh 'chmod +x -R ./bashScripts/Installkubectl.sh '
                 sh '  ./bashScripts/Installkubectl.sh '
                sh '  ./bashScripts/CheckIfEksctlIsExist.sh '

            }
        }
        stage("Create EKS cluster"){
            steps{

                    withCredentials([aws(accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'aws', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY')]) {
                        sh 'chmod +x   ./bashScripts/CreateCluster.sh '
                        sh './bashScripts/CreateCluster.sh'

                     }
              
            }
            
        }
stage('create kubecontext file') {
      steps {
        withCredentials([aws(accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'aws', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY')]) {

          sh 'aws eks update-kubeconfig --region us-east-2 --name Monitoring-kubernetes-cluster-1'
          sh 'kubectl get nodes'

        }
      }

    }
    stage("Install Helm"){
        steps{
                sh 'chmod +x   ./bashScripts/get_helm.sh  '
                sh '''#!/bin/bash 
                if [[ $(./bashScripts/get_helm.sh ) == *already* ]]
                then
                 echo "there" 
                else 
                 ./get_helm.sh 
                fi
                '''

        }
            }
     

    
    }

}

  