```mermaid
---
config:
  theme: default
---
architecture-beta

cards:
  tm: "Azure Traffic Manager"
  eastus: "East US Region"
  westus: "West US Region"
  eusvnet: "VNet East US"
  wusvnet: "VNet West US"
  euswebapp: "Web App East US"
  wuswebapp: "Web App West US"
  euspe: "Private Endpoint"
  wuspe: "Private Endpoint"
  acr: "Azure Container Registry\nBasic Tier"
  kv: "Key Vault"
  gh: "GitHub Repository"
  gha: "GitHub Actions"

containers:
  east_us:
    label: "East US"
    cards: [eastus, eusvnet, euswebapp, euspe]
  west_us:
    label: "West US"
    cards: [westus, wusvnet, wuswebapp, wuspe]
  shared:
    label: "Shared Services"
    cards: [acr, kv]
  cicd:
    label: "CI/CD"
    cards: [gh, gha]

connections:
  traffic_distribution:
    - from: tm
      to: [eastus, westus]
  east_flow:
    - from: eastus
      to: eusvnet
    - from: eusvnet
      to: euswebapp
    - from: euswebapp
      to: euspe
  west_flow:
    - from: westus
      to: wusvnet
    - from: wusvnet
      to: wuswebapp
    - from: wuswebapp
      to: wuspe
  shared_services:
    - from: acr
      to: [euswebapp, wuswebapp]
    - from: kv
      to: [euswebapp, wuswebapp]
  deployment:
    - from: gh
      to: gha
    - from: gha
      to: acr

styling:
  azure:
    fill: "#0072C6"
    stroke: "#fff"
    color: "#fff"
  network:
    fill: "#008272"
    stroke: "#fff"
    color: "#fff"
  security:
    fill: "#CA2171"
    stroke: "#fff"
    color: "#fff"

styles:
  - selector: [tm, eastus, westus, euswebapp, wuswebapp, acr, kv]
    style: azure
  - selector: [eusvnet, wusvnet, euspe, wuspe]
    style: network
  - selector: [gh, gha]
    style: security
```
