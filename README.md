# az-private-linky-aks

Example project to showcase [SAP Private Link service](https://help.sap.com/viewer/product/PRIVATE_LINK/CLOUD) integration with a workload hosted on [Azure Kubernetes Service](https://learn.microsoft.com/azure/aks/intro-kubernetes).

Main project can be found [here](https://github.com/MartinPankraz/az-private-linky). Associated blog series supporting the overall narrative and individual integration targets for SAP Private Link Service for Azure [here](https://blogs.sap.com/2021/12/29/getting-started-with-btp-private-link-service-for-azure/).

## Configure a private integration between SAP Business Technology Platform and your workload on Azure Kubernetes Service

> **Warning**⚠️
>
> This example assumes a configuration with a **single-service deployment** with NGINX. Hence the Private Link Service annotations are maintained **on the service level**. In case you prefer an Ingress Controller, **the annotations need to be maintained there**. Any Ingress Controller needs to be configured individually. See [here](https://learn.microsoft.com/azure/aks/ingress-basic?tabs=azure-cli) for more details. Complete your YAML with the annotations maintained from the shared snippet in [this repos](https://github.com/MartinPankraz/az-private-linky-aks/blob/main/app/nginx-ingress-example.yml).

1. Create an [AKS cluster](https://learn.microsoft.com/azure/aks/learn/quick-kubernetes-deploy-portal?tabs=azure-cli#create-an-aks-cluster)

2. Choose ingress flavor for your AKS in light of Azure Private Link Service:

- [Standard Azure load balancer](https://learn.microsoft.com/azure/private-link/private-link-service-overview)
- [Ingress Controller for AKS](https://learn.microsoft.com/azure/aks/ingress-basic?tabs=azure-cli)
- [Azure Application Gateway](https://learn.microsoft.com/azure/application-gateway/private-link-configure?tabs=portal) (will be discussed in next post on the [series](https://blogs.sap.com/2021/12/29/getting-started-with-btp-private-link-service-for-azure/))

The following steps apply to the standard Azure load balancer option and single service deployment.

3. Run `kubectl apply -f deployment.yaml`
4. Run `kubectl apply -f service.yaml`. Learn more about the Private Link Service configuration options for AKS [here](https://cloud-provider-azure.sigs.k8s.io/topics/pls-integration/).
5. Check your configuration with `kubectl describe svc hello-btp-service`
6. As of this step the process is identical to the standard process. Finish the handshake by completing the link from SAP BTP and approving the connection request from the PLS UI on AKS. See the [SAP docs](https://help.sap.com/docs/PRIVATE_LINK/42acd88cb4134ba2a7d3e0e62c9fe6cf/e8bc0c6440834a47a0ff57cb4efc0dc2.html) or the [first post of the blog series](https://blogs.sap.com/2021/07/02/whatever-happens-in-an-azure-and-btp-private-linky-swear-stays-in-the-linky-swear/) for more details.

## SAP BTP Destination configuration

Without SSL setup on NGINX, ingress controler or Azure Application Gateway you need to fallback to http for your integration test

key | value |
--- | --- |
Name | aks |
Type | HTTP |
URL | http://[your private hostname]/ |
Proxy Type | PrivateLink |
Authentication | [based on your service needs] |

### Additional Properties
key | value |
--- | --- |
TrustAll | true |
HTML5.DynamicDestination | true |
WebIDEEnabled | true |
WebIDEUsage | odata_abap |

## Become truly private and encrypted

- Continue your journey with a fully private AKS cluster [here](https://learn.microsoft.com/azure/aks/private-clusters)
- Add SSL to your AKS hosted workload using [NGINX](https://www.nginx.com/blog/nginx-ssl/) or [Mesh](https://learn.microsoft.com/azure/aks/servicemesh-about). See the [AKS ingress controller docs](https://learn.microsoft.com/azure/aks/ingress-tls?tabs=azure-cli) for more details.

## Hints on troubleshooting

- [Azure Private Link Connectivity troubleshooting guide](https://learn.microsoft.com/azure/private-link/troubleshoot-private-link-connectivity)
- Test connectivity without XSUAA first and don't make to many configurations at the same time

