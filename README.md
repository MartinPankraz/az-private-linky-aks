# az-private-linky-aks

Example project to showcase SAP Private Link service integration with a workload hosted on Azure Kubernetes Service.

Main project can be found [here](https://github.com/MartinPankraz/az-private-linky). Associated blog series supporting the overall narrative and individual integration targets for SAP Private Link Service for Azure [here](https://blogs.sap.com/2021/12/29/getting-started-with-btp-private-link-service-for-azure/).

## Configure a truly private integration between SAP Business Technology Platform and your workload on Azure Kubernetes Service

Learn more about the PLS configuration options [here](https://cloud-provider-azure.sigs.k8s.io/topics/pls-integration/).

- Create an [AKS cluster](https://learn.microsoft.com/azure/aks/learn/quick-kubernetes-deploy-portal?tabs=azure-cli#create-an-aks-cluster)

Choose ingress flavor for your AKS in light of Azure Private Link Service:

- Standard Azure load balancer
- Ingress Controller for AKS
- Azure Application Gateway

The following steps apply to the Standard Azure load balancer option and single service deployment.

- Run `kubectl -f deployment.yaml`
- Run `kubectl -f service.yaml`
- Check your configuration with `kubectl describe svc hello-btp-service`
- As of this step the process is identical to the standard process. Finish the handshake by completing the link from SAP BTP and approving the connection request from the PLS UI on AKS. See the [SAP docs](https://help.sap.com/docs/PRIVATE_LINK/42acd88cb4134ba2a7d3e0e62c9fe6cf/e8bc0c6440834a47a0ff57cb4efc0dc2.html) or the [first post of the blog series](https://blogs.sap.com/2021/07/02/whatever-happens-in-an-azure-and-btp-private-linky-swear-stays-in-the-linky-swear/) for more details.

- Continue your journey with a fully private AKS cluster [here](https://learn.microsoft.com/azure/aks/private-clusters)
- Add SSL to your AKS hosted workload using [NGINX](https://www.nginx.com/blog/nginx-ssl/) or Mesh. See the [AKS ingress controller docs](https://learn.microsoft.com/azure/aks/ingress-tls?tabs=azure-cli) for more details.
