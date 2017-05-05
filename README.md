# helm-spotinst-api-access

This is a Helm chart for Kubernetes that creates the following resources:

*Service Account*
The service account will be used to grant Spotinst access to the Kubernetes API. Note, this will in turn create a Kubernetes secret with a base64-encoded token which will be used to authenticate your Elastigroup to the Kubernetes API.

*Cluster Role*
The cluster role specifies the resources and actions that Spotinst needs to access within your Kubernetes cluster.

*Role Binding*
The role binding attaches the cluster role to the service account granting the appropriate access.

You will use the Kubernetes integration in your Elastigroup with the following values:

Host: Public ELB Hostname
Token: ````echo $(kubectl get secret $(kubectl describe serviceaccounts spotinst-api-access | grep Tokens | awk '{print $2}') --template='{{.data.token}}') | base64 -d````
