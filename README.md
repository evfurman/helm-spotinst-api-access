# helm-spotinst-api-access

This is a Helm chart for Kubernetes that creates the following resources:

###### Service
The service will create an external ELB (whitelisting only the Spotinst network ranges) to forward requests to the tectonic-lb pod.

###### Service Account
The service account will be used to grant Spotinst access to the Kubernetes API. Note, this will in turn create a Kubernetes secret with a base64-encoded token which will be used to authenticate your Elastigroup to the Kubernetes API.

###### Cluster Role
The cluster role specifies the resources and actions that Spotinst needs to access within your Kubernetes cluster.

###### Role Binding
The role binding attaches the cluster role to the service account granting the appropriate access.
<br />
<br />
You will use the Kubernetes integration in your Elastigroup with the following values:

Host: ````kubectl describe svc spotinst-api-access -n=tectonic-system | grep ^LoadBalancer | awk '{print $3}'````
<br />
Token: ````echo $(kubectl get secret $(kubectl describe serviceaccounts spotinst-api-access | grep Tokens | awk '{print $2}') --template='{{.data.token}}') | base64 -d````
