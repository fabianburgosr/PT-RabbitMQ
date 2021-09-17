
pipeline {
environment {
  nameSpace="rabbitmq"
  releaseName="rabbitmq-pt"
  }
  
  	agent {
    		kubernetes {
            cloud 'kubernetes'
      			inheritFrom 'default'
      			idleMinutes 5  // how long the pod will live after no jobs have run on it
      			yamlFile 'build-pod.yaml'  // path to the pod definition relative to the root of our project 
      			defaultContainer 'helm'  // define a default container if more than a few stages use it, will default to jnlp container
    		}
  	}
 
    stages {          
           stage('Deploy Rabbitmq to K8S') {
             
            steps {
                echo 'Deploy RabbitMQ to Admin K8s Cluster ....'
              container('helm'){
                /* Funciona con el plugin de Kubernetes deployment de Azure -Actualmente tiene un bug-
                    script {
          		kubernetesDeploy (configs: 'deployment.yaml',kubeconfigId: 'kubeconfdigoce')
        		    }*/
        		    
        		    //workaround=> use helm hasta que actualicen el plugin kubernetesDeploy

        		    //sh '/tmp/test.sh helm install nginx-ingress-${chartsName} nginx-stable/nginx-ingress --set controller.publishService.enabled=true,controller.hostNetwork=true,controller.service.type="" --namespace wso2mi --kubeconfig=/tmp/.kube/config'
                sh 'helm repo add bitnami https://charts.bitnami.com/bitnami'
        		    sh 'helm repo update'
                sh 'helm install ${releaseName} bitnami/rabbitmq  --values customvalues.yaml --namespace ${nameSpace}'
        		    
            }
             }   
           }
    }
}
