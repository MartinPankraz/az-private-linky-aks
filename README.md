# az-private-linky-aks
Example project to showcase SAP Private Link service integration with a workload hosted on Azure Kubernetes Service.

Main project can be found [here](https://github.com/MartinPankraz/az-private-linky). Associated blog series supporting the overall narrative and individual integration targets for SAP Private Link Service for Azure [here](https://blogs.sap.com/2021/12/29/getting-started-with-btp-private-link-service-for-azure/).

## Configure a truly private integration between SAP Business Technology Platform and your workload on Azure Kubernetes Service

- Create a [private AKS cluster](https://learn.microsoft.com/en-us/azure/aks/private-clusters)
- Use kubectl to apply the shared YAML and spin up the private link for SAP BTP
- Finish the handshake by completing the link from SAP BTP
