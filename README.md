# Helm-Chart-API-server


## For creating helm chart
`helm create http-api-server`

## For checking the helm directory tree structure
`tree http-api-server/`
output:

http-api-server/
├── charts
├── Chart.yaml
├── templates
│   ├── deployment.yaml
│   ├── _helpers.tpl
│   ├── hpa.yaml
│   ├── ingress.yaml
│   ├── NOTES.txt
│   ├── serviceaccount.yaml
│   ├── service.yaml
│   └── tests
│       └── test-connection.yaml
└── values.yaml

3 directories, 10 files



## In values.yaml file edit the image and service port

image:
  repository: neajmorshad/http-api-server:0.0.2  #update here 
service:
  type: ClusterIP
  port: 8080 # update here 

Note :You should have a docker image of your application uploaded into the docker hub


# In templates/deployment.yaml
# Update the image value as given below (remove extra info)
`image: "{{ .Values.image.repository }}"`


# You don't have to edit in Chart.yaml, sevice.yaml, 
# Your configuration values will come from values.yaml, you can check the service.yaml, deployment.yaml with its actual values before running the helm install command.



`cd ..`
`helm template http-api-server/`

After running the above command it should return you will service.yaml, deployment.yaml and test-connection.yaml with actual values

There is one more sanitary command lint provided by helm which you could run to identify possible issues forehand.

`helm lint http-api-server/`

# helm -debug -dry-run
The next check which we are going to do is -dry-run. 
Helm is full of such useful utility which allows developer to test its configuration
before running the final install command

Use the following -dry-run command to verify your Spring Boot Helm Chart

`helm install http-api-server --debug --dry-run http-api-server`




# helm install
`helm install my-http-api-server-first-release http-api-server`


"my-http-api-server-first-release" is the release name
"http-api-server" is out actual chart name 


# Verify the helm install
helm list -a

kubectl get all
you will see the pod:
pod/my-http-api-server-first-release-677c8f76dd-s7bww


Now if you update the replica count or some others update the version and run
`helm upgrade my-http-api-server-first-release .`


helm rollback my-http-api-server-first-release 1

helm delete my-http-api-server-first-release


# you can follow this tutorial for creating helm chart for your application 
https://jhooq.com/building-first-helm-chart-with-spring-boot/









