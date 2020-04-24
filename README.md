## AWS Elastic Kubernetes Service - Blue Green Deployment

In this project you will apply the skills and knowledge which were developed throughout the Cloud DevOps Nanodegree program. These include:

* Working in AWS
* Using Jenkins to implement Continuous Integration and Continuous Deployment
* Building pipelines
* Working with CloudFormation to deploy clusters
* Building Kubernetes clusters
* Building Docker containers in pipelines

---
### Setting your AWS infrastructure

For deploy your infrastructure execute the next script inside cloudformation/ folder:

    sh ./create.sh CloudDevOpsCapstone network_and_eks.yml network_and_eks.json
    
Note: The creation of EKS cluster takes almost 10 minutes

### Setting your pipeline for lint, build and publish your docker image

For create your pipeline you have to add the file `Jenkinsfile` in jenkins, also before run the pipeline you have to do login in Docker for publish image task

### Blue Green deployment configuration is setting in Kubernetes using Controllers and Service

1) Apply blue controller inside blue-green/blue folder
    
    `kubectl apply -f blue-controller.json`
    
2) Apply green controller inside blue-green/green folder
    
    `kubectl apply -f green-controller.json`
    
3) Deploy service in blue-green/ folder

    `kubectl apply -f blue-green-service.json`
    
   Then you can check the application deployed in your browser
    
4) For do a blue-green deployment update the section to **green** in blue-green-service.json file:


    "selector":{
          "app":"blue" 
        },

5) Deploy again the service

    `kubectl apply -f blue-green-service.json`
    
    You can see how each POD is updated to the green version incrementally

---
