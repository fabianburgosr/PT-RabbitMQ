
pipeline {
environment {
  chartsName="rabbitmq"
  }
 
    stages {          
           stage('Deploy Rabbitmq to K8S') {
       		
            steps {
                echo 'Deploy RabbitMQ to Admin K8s Cluster ....'
                /* Funciona con el plugin de Kubernetes deployment de Azure -Actualmente tiene un bug-
                    script {
          		kubernetesDeploy (configs: 'deployment.yaml',kubeconfigId: 'kubeconfdigoce')
        		    }*/
        		    
        		    //workaround=> use helm hasta que actualicen el plugin kubernetesDeploy
        		    //sh '/tmp/test.sh helm repo add nginx-stable https://helm.nginx.com/stable'
        		    //sh '/tmp/test.sh helm repo update'
        		    //sh '/tmp/test.sh helm install nginx-ingress-${chartsName} nginx-stable/nginx-ingress --set controller.publishService.enabled=true,controller.hostNetwork=true,controller.service.type="" --namespace wso2mi --kubeconfig=/tmp/.kube/config'
        		    sh '/tmp/test.sh helm install ${chartsName} ./helmcharts/${chartsName} --namespace rabbitmq'
        		    //sh '/tmp/test.sh  helm install ${chartsName} ./helmcharts/${chartsName} --namespace wso2mi --dry-run --debug --kubeconfig=/tmp/.kube/config'
               	    }
            }
           }
    }
}
