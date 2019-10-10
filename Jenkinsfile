pipeline{
    agent any
 
stages
    {
    stage('Git Checkout')
    {
         steps
        {
             checkout scm
        }
    }
     stage('terraform init') {
            steps {
		  
		   
                 sh "terraform init -input=false"
		 
               
            }
        }
        
         stage('terraform plan') {
            steps {
		     wrap([$class: 'MaskPasswordsBuildWrapper']) {
        
sh "terraform plan  -input=false -var subscription_id=${AZURE_SUBSCRIPTION_ID} -var tenant_id=${AZURE_TENANT_ID} -var client_id=${AZURE_CLIENT_ID} -var  client_secret=${AZURE_CLIENT_SECRET}  -var resource_group_name=${resource_group_name} -var location=${location}"  
    }
	
               
            }
        }
        stage('terraform apply') {
           steps {
		 wrap([$class: 'MaskPasswordsBuildWrapper']) {
               
			 
             sh "terraform apply -input=false -auto-approve  -var subscription_id=${AZURE_SUBSCRIPTION_ID} -var tenant_id=${AZURE_TENANT_ID} -var client_id=${AZURE_CLIENT_ID} -var  client_secret=${AZURE_CLIENT_SECRET}  -var resource_group_name=${resource_group_name} -var location=${location} "

		 }
           }
        }
    
}
}
