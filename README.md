# helm-spotinst-api-access

This is a Helm chart for Kubernetes that creates the following resources:

*ALB Ingress Resource*
The ALB ingress resource is responsible for creating a public Application Load Balancer in the specified region with the required resources and a Route 53 address in the public hosted zone. Note, you will need to already have the ALB Ingress Controller running in your Kubernetes cluster for this to work. More information on this resource can be found at: https://github.com/coreos/alb-ingress-controller.

*Service Account*
The service account will be used to grant Spotinst access to the Kubernetes API. Note, this will in turn create a Kubernetes secret with a base64-encoded token which will be used to authenticate your Elastigroup to the Kubernetes API.

*Cluster Role*
The cluster role specifies the resources and actions that Spotinst needs to access within your Kubernetes cluster.

*Role Binding*
The role binding attaches the cluster role to the service account granting the appropriate access.

You will use the Kubernetes integration in your Elastigroup with the following values:

Host: spotinst-api.cluster.{{.Values.vpc}}.{{.Values.region}}.{{.Values.domain}}
Token: { Token value from kubernetes secret file }
